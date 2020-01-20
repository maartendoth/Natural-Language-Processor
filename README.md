# Natural-Language-Processor
 A very basic Natural Language Processor (in bash)
 
I have create a small corpus of about 23k+ lines. containing short, beginner level French sentences, and phrases.
I'm now in the processes of creating a 'poor man's natural language processor' script in bash. The idea is to create a script that can automatically transform the corpus into a list with all the meaningful words and phrases used in the text. So that the resulting list can be used for creating language learning materials, based on the original corpus.
Im first focusing on the French languages, and preferable it should work on any French body of text. And when finished, the idea is to retractor away all the French language specific stuff in such a way that the NLP can be reused on other languages in the future.

I have sanitized the text, mostly, but the main issues i’m still having are:

* identify words as; a sound an animals make
* identify words as; common used sounds that are not actual words (eg. ahh, oh, auw, etc)
* which capitals are meaning full ( names, or otherwise)
* finding word stems

Some of these problems could be negated, by looking the words and phrases up in a dictionary.
But to do that, in need to split the text up in to words and word phrases that will match a dict entry. For example the English phrase 'piss off' is a rude way of commanding someone to go away. But looking up the words 'piss' and 'off' will not work. You will need to search for the whole phrase 'piss off'. So then the question is how to know which words devided by space should be considered one phrase. 

And the English word "don't" is actually an contractions of the words 'do' + 'not'. so the other question is how to know if a words is a contraction and what the two contracting words are. This is more complex then it sounds because the french language is using contrations for such a long time that some of phrases that where consider contrations, over time became lexicalized to one word. For example: aujourd'hui 'today' deriving from au jour de hui, similar to Spanish al día de hoy, Italian al giorno d'oggi, literally 'at the day of today' and meaning 'nowadays,' but hui is no longer recognized as a meaningful word in modern French. 

And the main other issues are words glued together with - (hypens), and words written in all caps.

## solving the 'unique word phrase' problem
I think the 'words glued together with hypens' and the "contracted words with the ' mark" could be solve by knowing the grammar rules. (which i don't)
And the problem of finding word phrases could (possibly) be solves with ngrams, (but i’m not really sure how exactly. so i’m leaving this for last)

### ' (Apostrophe)
Rules ??:
If the second character in a word is, print the word including the the previous word as a phrase to a list. it is most likely and contractions
' is never the first character, and i found only one entry where it was the last character: "l'ambulance va à l'". but i’m not sure if that is a compete sentence.
If ' is encapsulated by two letters and it is the 3 or higher character in the word, its most likely a normal French word.
L' = le; l'homme = le homme
Is an ' always an abbreviation of "e"
What about words like: qu'elle and qu'il ?
Do French word with two ' ' exist?

### - (hyphen)
some examples and use cases:
Lowercase - lowercase; probably a word
Lowercase - uppercase; probably a name
-°c (not containing letters); probably a notation or measurement
Multiple - in one word; probably a phrases or a word written with hypens as syllables indicators
-aaah- (enclosing a word); probably an unusual expression
- oh non; a typo ??
' - ' (word space hypen space word); some sort of phrase?

### Finding word phrases
I already have a script that can find n-number of ngrams (as much as i want or there are words in the sentence). and i remove all ngrams that are only found once.
But i’m not sure, how to further process the results. 

### Dictionary / word-list
To be able to look words up in a word-list, i like to aggregate lists of known French words and phrases, and build them into one big list. For the first step, it does not even need to be a dict entry, just a list of known French words is enough to filter out all typo’s, animal sounds, other sounds, uncommon names, etc.

## Notes
The above mentioned problems are the ones i’m focusing on right now, and which i want to solve before worrying about how to further process the main corpus.

## Problems

I have extracted the lines form the text that contain at least one item that is problematic. And grouped them in separate files. For each of these problems i still need to implement a solution.

- [problems/-/-](https://github.com/maartendoth/Natural-Language-Processor/tree/master/problems/-/-)
- [problems/…/…](https://github.com/maartendoth/Natural-Language-Processor/tree/master/problems/%E2%80%A6) 
- [problems/'/'](https://github.com/maartendoth/Natural-Language-Processor/tree/master/problems/') 
- [problems/œ/œ](https://github.com/maartendoth/Natural-Language-Processor/tree/master/problems/%C5%93) 
- [problems/non-alphabetical](https://github.com/maartendoth/Natural-Language-Processor/blob/master/problems/non-alphabetical) 
- [problems/only-uppercase](https://github.com/maartendoth/Natural-Language-Processor/blob/master/problems/only-uppercase)

The general question for these problems is, how to further processes these lines.

### œ
It turned out that this is not a real problem, it seems to be an actual valid French letter. 

### …
This seems simple, but I am not sure how this is used. I guess though that someone who actually understands French could easily explain this. 

### ' (Apostrophe)
After asking many people and searching online, I finally found a list with french grammar rules that explain the usage in such a way that I can start with creating a script to extract the correct words out of items containing a hyphen. The most important question now, does this info include all use-cases and all exceptions to the rule?

https://fr.wikipedia.org/wiki/%C3%89lision https://en.wikipedia.org/wiki/Elision
https://www.lawlessfrench.com/pronunciation/elision/
https://www.lawlessfrench.com/pronunciation/contractions/
https://www.lawlessfrench.com/grammar/informal-pronouns/
https://french.kwiziq.com/revision/glossary/contraction/l-elision-elision

### - (hyphen)
This doesn’t look to difficult, but im just not sure what these French lines are supposed to express. Need advice from a French speaker.

### Non-alphabetical
The easiest would be to simply remove all these characters, but I like to first find out if some of these characters add so much meaning that its better to keep them. 

### only-uppercase
I’m not sure what to make of this jet.

## To-do list
Find a better way to deal with punctuation. Simply removing them, as I have now, might give false positive during n-gram processing. (so this needs to be addressed, before continuing with ngrams).

Currently, the corpus is created and processed line-by-line as they appeared in sources files. This is because many lines, especially those from; chats, tweet, short posts and subtitles, don’t always have punctuations or clear sentence endings. But if I could have a script that removes all line-breaks, and then cut the text into sentences, and add commas where their should be one, and capitalize the first letter, then that would improve the quality of the aggregated corpus.

## Scripts

- [Scritps/ngrams](https://github.com/maartendoth/Natural-Language-Processor/blob/master/scritps/ngrams) 

### ngrams
I have a simple script that can build ngrams. 
Still need to find a good way of dealing with punctuations.
And I found information on how to calculate weighted probability (this is not implemented jet):

https://en.wikipedia.org/wiki/N-gram
https://blog.xrds.acm.org/2017/10/introduction-n-grams-need/ (how to calculate bigrams)
https://sookocheff.com/post/nlp/n-gram-modeling/ (how to calculate ngrams)
https://web.stanford.edu/~jurafsky/slp3/4.pdf
[](/tree/master/problems/') 