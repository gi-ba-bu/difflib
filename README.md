## `ratio_min`

### A new function named `.ratio_min` is added to the python library difflib.

---

`.ratio_min(self,m)` is an extension of the difflib's function `.ratio(self)`. Equivalently to `.ratio(self)`, `.ratio_min(self,m)` returns a measure of two sequences' similarity (float in [0,1]).
In addition to .ratio(), it can ignore matched substrings of length less than a given threshold m.

The score is calculated as 2\*M_min / T.

Where T is the total number of characters (both sequences), and
M_min is the number of elements matched with every single match having at least m consecutive characters.

Equivalently to `.ratio()`, `.ratio_min()` is applied to the output of `SequenceMatcher(None, a, b)` where `a`, `b` are the two sequences being compared.

Note that this is 1 if the sequences are identical, and 0 if
they have no substring of length m or more in common.
In addition, `.ratio_min(1)` is equivalent to `.ratio()`.

---

## Basic use example

```
 >>> s = SequenceMatcher(None, "abcd", "bcde")
 >>> s.ratio() # "bcd" matched to "bcd"
 0.75
 >>> s.ratio_min(1) # "bcd" matched to "bcd"
 0.75
 >>> s.ratio_min(2) # "bcd" matched to "bcd"
 0.75
 >>> s.ratio_min(3) # "bcd" matched to "bcd"
 0.75
 >>> s.ratio_min(4) # No match of length 3 or more consecutive characters
 0.0
```

## A simple use case

---

### Consider the following use case. We want to compare a given string to a given list of strings.

We would like to match the book title "Animal farm" to the string "Animal farm book".

```
>>> string = 'Animal farm'
>>> strings = ['A nominal farm', 'A minimal farm', 'Animal farm book']
```

The resulting similarity scores between "Animal Farm" and each string in `strings` are:

|              | A nominal farm | A minimal farm | Animal farm book |
| ------------ | -------------- | -------------- | ---------------- |
| ratio()      | 0.800          | **0.880**      | 0.815            |
| ratio_min(1) | 0.800          | **0.880**      | 0.815            |
| ratio_min(2) | 0.560          | 0.800          | **0.815**        |
| ratio_min(3) | 0.560          | 0.800          | **0.815**        |

This approach results is a wider gap in similarity scores.

### An alternative approach: starting and ending each string with a space.

This approach can help focusing on full words.

```
>>> string = ' Animal farm '
>>> strings = [' A nominal farm ', ' A minimal farm ', ' Animal farm book ']
```

|              | A nominal farm | A minimal farm | Animal farm book |
| ------------ | -------------- | -------------- | ---------------- |
| ratio()      | 0.828          | **0.897**      | 0.839            |
| ratio_min(1) | 0.828          | **0.897**      | 0.839            |
| ratio_min(2) | 0.690          | **0.897**      | 0.839            |
| ratio_min(3) | 0.552          | 0.759          | **0.839**        |

---

Note that, the original library, named difflib, contains several other functions, here not reported.
