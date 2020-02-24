# Guide to Unix and Linux

## C20: Regular Expressions
- matching lines and words
```
grep '^Harley' data
grep 'Harley$' data
grep '^S' data | wc -l
grep -w 'cat' data
grep '\<know\>' data
```

- matching characters, character classes
```
grep 'Har..y' data
grep 'H[aA]' data
grep 'X[0-9][0-9]' data
grep 'X[^ao]' data
```
- Using ranges and predefined character classes
```
grep 'h[a-z]' data
grep '[a-z][0-9][a-z] [0-9][a-z][0-9]' data
```
- repetition operators
```
grep 'H[a-z]*' data
grep 'error.*code' data
grep ':.*:' data

grep 'variable[0-9]+' data #?

grep 'colou?r' data
```


## MISC
- 查看inode信息
```
stat hello.c
```

- strong quote''? weak quote""?

- setting C collating sequence
```
export LC_COLLATE=c
export LC_COLLATE=POXIX
```

