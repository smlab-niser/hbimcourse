---
title: "Models"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

The way the HBIM is setup, one may add potentially new data to the HBIM and improve
on it. In this section, we will go through two similar exercises to improve the HBIM
and it's quering capabilities.

## Example I: Transcripts of the documents
In this example, we will directly retrieve the data from the database and modify
it.

The HBIM database contains the documents in various format. However, searching
through the documents is not possibe since they are not computer readable. There
are capable OCR programs that can read the documents with higher degree of accuracy.

In this example, we will use Tesseract to OCR. It is a open source program based
on LSTM neural network. It is based on `libtesseract` written in C++. However, there
are frontend for many programming language like Python. We may use any tooling or
programming language to interact the database, irrespective of what the API is written
in.

### Setting up the database
Taking a look at the database, we can see that the relation is defined as,
```sql
CREATE TABLE documents(
        id                SERIAL PRIMARY KEY,
        description       TEXT,
        filetype          CHAR(8),
        file              CHAR(20),
        comments          TEXT,
        top_left          POINT,
        bottom_right      POINT
);
```

There is no place to add the transcripts. Therefore, we will add a new attribute
to add the transcript. If the document is several pages long, it makes sense to
store the transcripts separated by pages. One long text for the transcript for the
entire document may difficult to query in case there is a mistake in the OCR.

Here we will create a new relation to store the transcript of the documents.

```sql
CREATE TABLE transcripts (
	id        SERIAL PRIMARY KEY,
	texts     TEXT,
	doc_id    INT REFERENCES documents(id),
	page      INT
);
```

where the `texts` contains the transcripted text, `doc_id` is a foreign key to the
`documents` relation and the `page` contains the page number in the document.

The database is now ready to be able to add new contents, which we do in the next
section.

### Setting up tesseract

### Populating the database with transcript

### Advantages
- There is less overheat since the data is accessed directly.
- Any programming language can be used, as long as they can interface with database
management server.

### Disadvantages
- Knowledge of the internal working of the database is required.
- If the database has been significantly changed, then the API may need to be updated.
