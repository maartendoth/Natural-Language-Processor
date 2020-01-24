### Language_filter
it should have the ability to:

* filter out all words that contain characters that are not part of the character set/class for that specific language.
* recognize all letter combination that do not exist in that language.

To do the letter combination recognition you need to have an n-gram database of all letter combination found in the language and it should take into account digraphs and trigraphs
 (letter combination) that are pronounced as a phoneme (one sound) and possibly even letter groups that have fixed sounds. And change letter combinations to a capital letter from an other alphabet (maybe Greece alphabet?).

https://en.wikipedia.org/wiki/French_orthography#Digraphs_and_trigraphs
https://www.mimicmethod.com/french-pronunciation-ultimate-guide/

### punctuation_filter
unfortunately most people do not use all the punctuation where they should, and can come up with very creative ways of using punctuation marks. 
Need to figuer out how to deal with punctuation

### Case_filter
detect meaningful capitals (some times words are not capitalized where they should and vise versa.)
Names and especially companies names do not necessarily represent the correct French spelling.
Need to figure out how to deal with letter cases

### number_filter
* transform all roman numerals to the correct Unicode equivalent
* transform all written numbers to digits