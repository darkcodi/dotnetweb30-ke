# Blaming \(annotate\)

The high-level function of `git blame` is the display of author metadata attached to specific committed lines in a file. This is used to examine specific points of a file's history and get context as to who the last author was that modified the line. This is used to explore the history of specific code and answer questions about what, how, and why the code was added to a repository.

`$ git blame file  
566a0863 (Alex Blewitt 2011-07-12 09:43:39 +0100 1) First line  
ed0a7c55 (Alex Blewitt 2011-07-12 09:43:51 +0100 2) Second line  
8372b725 (Alex Blewitt 2011-07-12 09:44:06 +0100 3) Third line  
ed0a7c55 (Alex Blewitt 2011-07-12 09:43:51 +0100 4)`

