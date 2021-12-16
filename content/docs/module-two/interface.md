---
title: "Interface"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# Setting up the interface

We will use the Python programming language to build the interface for the HBIM.
Python programming language can be downloaded from the official site and the installation
instruction differs from different operating systems. For Linux and Mac OS X, the
recommeded way of installing the programming langauage is the default package manager.

However, there are independent package manager like
[Miniconda](https://conda.io/miniconda.html) that help install different versions
of python and many python packages in a virtual environment without poisoning the
operating system's packages.

Since, the database management software is Postgres, we need to interface Postgres
from Python, for which we will need the `psycopg2` package from PyPI which can be
installed by issuing the command,
```
pip install psycopg2
```

## Connecting the database
Before we can connect to the database, we have to make sure that the database server
is up and running. The operating system init system generally starts the server daemon,
and can be checked by asking the it, (as root)
```
sv status postgres          # for other init system
systemctl status postgres   # for systemd init system
```
If the service is not running it can be started as switching to the `postgres` user
and giving the command `postgres`. Or adding as a service to the init system.

Once the database is up and running we can connect to the database using `psycopg2`.
```python
#!/bin/env python
import psycopg2 as pg;

db = pg.connect(
        host='localhost',
        database='hbim',
        user='postgres' );
```

Specific to the `psycopg2` package, all the database operation are executed as a
cursor command. To test if the database is working, we will execute the ''hello world''
program statement in SQL to display `Hello, World!` to the screen.
```python
cur = db.cursor();
cur.execute('SELECT "Hello, World!";');
for row in cur:
        print(row);
```
Since a `SELECT` statement in SQL usually returns tuples of the relation, the cursor
executes the query and stores as a Python list iterator which can be run through
a foreach loop to get individual tuples. And the tuple is a string constant,
```python
('Hello World!',)
```
which confirms that the database connection was successful. If you do not see the
above result, please make sure that the database server/daemon is running and the
`psycopg2.connect()` function exited successfully.

## Images
The database contains, the `images` relation and it is recommended that all the operation
on the images is performed through the interface. The interface must expose the following
functions

- Add new images to the database
- Add comments to the images
- Add placeholder to the images
- Add bookmarks to the images
- Remove an image from the database

The images are not stored as binary blobs in the database, but as a file in a central
repository.


