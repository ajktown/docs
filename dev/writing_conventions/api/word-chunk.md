# Word Chunk

## Overview

Wordy v1 used to save `dateAdded` as a number into the DB and sorted it with the help of `sem` (semester).

Wordnote v2 now will save both `dateAdded` and `createdAt` (Created automatically by mdb) into the DB.


Sorting mechanism stays the same.


When word is created, datedAdded will be also created, if not given.

Undoing deleting and reposting the word will use the same `dateAdded`, and this way the sort stays the same all the time.