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

# Setting up the database

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

To add support for comments in images, we need to store images as a relation in the
database. The relation database must contain the attribute for the comments as well
as the location in the image in pixels. For example, we can add a comment, like
"ruins" at the pixel position (100,100) or a region of space with the corners,
(100,100) and (200,200) pixel position. The comment can be stored as a string
`comment` attribute and the corners as `top_left` and `bottom_right` as points.
Points are a predefined datatype in Postgre.

As a primary key, we can add a `id` attribute to distinguish between tuples and to
refer from other relations as a foreign key. Postgres supports storing the images
as a binary blob in the database. But we want to avoid that. The most important
reason for not storing the data as a binary blob is that the image cannot be accessible
without the database. In case of a database corruption or database integrity issue,
the images will be lost. To prevent this, we store the image in a separate directory
and refer to it from the database. That attribute is a string called `file`.

We can add a description to the image as a string called the `description` attribute. With
that the entire relation for images would look like,

```sql
CREATE TABLE images (
        id                SERIAL PRIMARY KEY,
        description       TEXT,
        file              CHAR(20),
        comments          TEXT,
        top_left          POINT,
        bottom_right      POINT
);
```
