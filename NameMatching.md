# Introduction #

The best way to match two contacts is intersecate phone or mail, but

**how to understand if two different names N, FN, NICKNAME refers to same person**?

There're some algorithms that can help, one above other [NYSIIS](http://en.wikipedia.org/wiki/New_York_State_Identification_and_Intelligence_System) which is still implemented in a python module.

I'm still testing a way to rank the matching of two names using different f(nysiis(n))  using a comparableCard class...

> # Cases #
Here follows some data examples that we should try to match

```
N1: Obi Wan Kenobi
N2: Obi Wan
N3: Kenobi;Obi Wan


N4: obiwan.kenobi@resistence.org
N5: obiwankenobi@resistence.org
N6: obiwan@kenobi.org
```

N1-N3 are quite easy, it's about splitting and intersecting like the following
```
def matchName(n1,n2):
    s1Us2 = set(n1).intersection(set(n2))
    el = s1Us2.pop()
    i1 = n1.index(el)
    i2 = n2.index(el)
    n11 = n1[i1:]+n1[:i1]
    n21 = n2[i2:]+n2[:i2]
    print "".join(n11).strip()
    print "".join(n21).strip()
```

> We must be careful on single names (eg. given names only) that should be resolved manually.

N4-N6 needs some hinting and playing with nysiis.


> # Functions #
## set fraction ##

splitting both names by space we get two sets: {obi,wan,kenobi} and {obi,wan}
set\_score =  #intersection / #union;  (ex #{obi,wan} / #{obi,wan,kenobi} )

## list fraction ##
same as set, but with list.
list\_score = #intersection / avg(#set1, #set2) (ex. 2 / 2.5)