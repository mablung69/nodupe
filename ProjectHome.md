"One py to merge'em all"

I start to write NoDupe to merge infos from my mobiles and various PC addressbooks and, astonishly, it works for me very well.

It scrolls all vcards contained in one or more files: each time he found duplicate contacts (ex. same name, mail, phone) he merges info as loseless as possible.


> # How it works #

the ingredients:
  * All - a list of all contacts
  * Clean - a list of de-duped contact
  * merge(c1,c2) - a merge function, returns a merged item in c1
  * match(c1,c2) - a match function, returns true if c1 and c2 are the same person
  * the algorithm

the algorithm is almost the following:
```
for a in All:
  for c in Clean:
      if match(a,c):
         a=merge(a,c)
         break
      else:
         Clean.append(a)
```

> # Issues #
The issues are about:
  * match() - try to match all uppercase combination of NAME (N), FORMATTED NAME (FN), intersection of all phones (TEL) and all email (EMAIL)
  * merge() - joins TEL, MAIL and N of both contacts. If more FN are provided, the shortest one is set as NICKNAME

> # Ideas #
  * better matching strategies (eg using regex and/or fuzzy instead of True|False)
  * better merging strategies (recognize nicks, suffixes)
  * normalize contacts while parsing (ex. if no "N" or "FN" try to guess from "EMAIL")
  * organize contacts while parsing (eg, split "family" and "given" name)


This is the starting point but gives nice results for my 2500 contacts.

