# {{date:YYYY-MM-DD}}, {{date:dddd}}
## Journal

## Notes
#### Created today
```dataview
List FROM "Zettelkasten" WHERE file.cday = date("{{date:YYYY-MM-DD}}") SORT
file.ctime asc
```


#### Modified today
```dataview
List FROM "Zettelkasten" WHERE file.mday = date("{{date}}") SORT
file.ctime asc
```