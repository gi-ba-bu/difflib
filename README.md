## difflib2
### Here, (a portion of) the difflib Python library is improved with one additional function named .ratio_min() at line ~549.

---

`.ratio_min(self,m)` is an extension of the difflib's function `.ratio(self)`. Equivalently to `.ratio(self)`, `.ratio_min(self,m)` returns a measure of two sequences' similarity (float in [0,1]).
In addition to .ratio(), it can ignore matched substrings of length less than a given threshold m. 

The score is calculated as 2.0*M_min / T.

Where T is the total number of characters (both sequences), and
M_min is the number of elements matched with every single match having length at least m characters. 

Equivalently to .ratio(), .ratio_min() is applied to the output of SequenceMatcher(None, a, b) where a, b are the two sequences compared.

Note that this is 1 if the sequences are identical, and 0 if
they have no substring of length m or more in common.
.ratio_min() is similar to .ratio(). 
.ratio_min(1) is equivalent to .ratio().

---

### Use example

```
 >>> s = SequenceMatcher(None, "abcd", "bcde")
 >>> s.ratio_min(1)
 0.75
 >>> s.ratio_min(2)
 0.75
 >>> s.ratio_min(3)
 0.75
 >>> s.ratio_min(4)
 0.0
```
---
Note that, the original library, named difflib, contains several other functions, here not reported. 
