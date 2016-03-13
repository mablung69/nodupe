# Introduction #

## normalizeCard ##
Before processing a contact let's look at what it can be:
# a nice item
```
VCARD
N: Polli;Roberto
FN: Roberto Polli
NICKNAME: ioggstream
EMAIL: robipolli@gmail.com
EMAIL;TYPE=INTERNET: roberto.polli@email.it
```
# a not so nice item
```
VCARD
N: roberto roberto
FN: Roberto Polli
EMAIL: robipolli@gmail.com
```
# a bad item
```
VCARD
N:
EMAIL: robipolli@gmail.com
```

before trying to see if they are the same person, we've to make them up: so normalizeCard() put the latest item in a "better" way:
# a bad item
```
VCARD
N: robipolli@gmail.com
FN: robipolli@gmail.com
EMAIL: robipolli@gmail.com
```

## Match Card ##
todo: describe how to match two vcards

## Rank Fields ##
Now we got two normalized cards and we know they refer to the same person.
we have to chose between various names:
```
N: Polli;Roberto
N: roberto roberto
N: robipolli@gmail.com
```

to do that we need a Score(N) function that make us choiche the best one.
as of now Score works this way:
```
score = 0
# if it's a complete N object
if N.given:
   score += len(N.given)+1
   if N.family != N.given:
      score *= 1+len(N.family)
else:
#if it's a string...
   score = len(N)+1
   # if it's a (maybe) mail
   if score ~= "[@_;]":
      score = score/2
```

that's just brainstorming but results are good enough...
# Details #

Add your content here.  Format your content with:
  * Text in **bold** or _italic_
  * Headings, paragraphs, and lists
  * Automatic links to other wiki pages