---
title: "Database Design"
weight: 2
# bookFlatSection: false
bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# The database

There are many robust database management systems available like MySQL, MariaDB,
Oracle. But since we are only going to use open source tools, we will use
[PostgreSQL](http://www.postgresql.org). PostgreSQL is based on relational database
model and the create, read, update and delete (CRUD) operations are done using the
Structured Query Language (SQL).

## Getting the database
The official binary releases and source code can be found on at
[PostgreSQL](http://www.postgresql.org), which should be the preferred method of
installing the database software on Windows and Mac OS X. For Linux-based operating
systems, the package manager should be preferred.

Postgres uses a client-server model, unlike say Sqlite where the main program provides
both the user interface and the database management. The server for Postgres is program
called `postgres`. There are many clients for Postgres having both command-line and
GUI interfaces for Windows, Mac, Linux as well as the web, with both proprietary
and open-source license. In short, there are a lot of choices for the client, and
the official Postgres Wiki has a list, which can be found [here](https://wiki.postgresql.org/wiki/PostgreSQL_Clients).

## Setting up the database server
Once the installation is complete, the server can be invoked by simply issuing the
command `postgres`. However, the server will most likely fail to start because it
doesn't come pre-configured. The official Postgres documentation, which can be found
[here](https://www.postgresql.org/docs/14/runtime.html) explains how to configure
the Postgres server. We will not go into details, but for the sake of completeness
we will provide a minimal working example.

## Setting up the client
Among the myriad of clients available, we will use the official `pgsql` client that
is maintained by the Postgres developers. It is free, open source like the Postgres
server and it is a command-line interface. The client can be invoked by issuing
`pgsql` and logging in.

# Database design
There are 7 dimensions of HBIM and we want to store all the data so that they can
be easily accessed. While the API takes care of the data read and write operations,
there are cases when direct access to the database is desired. For instance, if we
want to run a algorithm to perform some task, say OCR, on all the scanned and collected
documents, then accessing the database directly is faster and easier, since we do
not have to worry about the API layer. However, the disadvantage of doing things
this way is that it requires knowledge about the internal database design.

In this section, we will be going through the database design process for storing
the various dimensions of the HBIM as well as the interplay of those dimensions that
depend on each other. At the outset, we want the HBIM to support the following
features,

- Support for adding comments and placeholder texts for images, videos, documents
and models.
- Support for bookmarks at various points and time.

## Images
As a primary key, we can add a `id` attribute to distinguish between tuples and to
refer from other relations as a foreign key. Postgres supports storing the images
as a binary blob in the database. But we want to avoid that. The most important
reason for not storing the data as a binary blob is that the image cannot be accessible
without the database. In case of a database corruption or database integrity issue,
the images will be lost. To prevent this, we store the image in a separate directory
and refer to it from the database. That attribute is a string called `file`.

We can add a description to the image as a string called the `description` attribute.
With that, the entire relation for images would look like,

```sql
CREATE TABLE images (
        id                SERIAL PRIMARY KEY,
        description       TEXT,
        file              CHAR(20),
        comments          TEXT,
);
```
As you can see, the file name is limited to 20 characters including the file extension.

## Comments
To add support for comments in images, we need to store images as a relation in the
database. The relation database must contain the attribute for the comments as well
as the location in the image in pixels. For example, we can add a comment, like
"ruins" at the pixel position (100,100) or a region of space with the corners,
(100,100) and (200,200) pixel position. The comment can be stored as a string
`comment` attribute and the corners as `top_left` and `bottom_right` as points.
Points are a predefined datatype in Postgres.

To store the comments, create the following relation,
```sql
CREATE TABLE comments (
        id            SERIAL PRIMARY KEY,
        description   TEXT,
        page          INT,
        top_left      POINT,
        bottom_right  POINT,
        type          ENUM,
        type_id       INT REFERENCES images(id) documents(id) video(id)
        time_stamp    TIMESTAMP,
);
```

The `page` and `time_stamp` attributes can be `NULL`. For documents, the comments
are given a location but they can also be at different pages. The `page` table
specifies at which page the comment is located. The `time_stamp` attribute does the
same for videos. The `type_id` is the foreign key to respective relation.

## Documents
The document can be stored same as the `images` relation with some extra attributes like
the file type. Images, irrespective of their file types are, generally supported
by image viewers. But for documents, there are different filetypes that need different
viewers. For example, a PDF viewer may not support DJVU files. So, we store the
file type in the database. With that, we can create the following relation,

```sql
CREATE TABLE documents(
        id                SERIAL PRIMARY KEY,
        description       TEXT,
        filetype          CHAR(8),
        file              CHAR(20),
        comments          TEXT,
);
```
Most of the filetypes have 3 characters extensions, but some have 4 or even 5 characters
extensions. Therefore to accomodate it, and future filetypes, we have allocated 8
characters in the database.

