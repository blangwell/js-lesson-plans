# LL3 Strings and Regular Expressions

## String Encoding
Before we get into it
Remember that any code that we write is ultimately broken down into numbers by the computer (either 1 or 0). 

it is the combination and arrangement of these 1s and 0s that allow us to express paragraphs of text,
the number 5 quintillion ,
or an online drum machine. 

keeping this in mind, inside of the computer strings are represented by numbers. encoding is simply a number or group of numbers that serve as a code to represent a specific character.

In prehistoric times, western characters were commonly encoded with ASCII 
or -> American Standard Code for Information Interchange

With ASCII encoding, 127 different unique numbers were available. This covered the english alphabet, numbers 0 - 9 and several symbols

A = 65
B = 66
…
Z = 90


In December 2007 Unicode overtook ASCII as the most commonly used encoding on webpages. In fact, you have been using it on your webpages maybe without knowing it. if you look at your HTML boilerplate, you’ll see charset=UTF-8 in the <head> 


## Regex password validation step by step
[Regexr](https://www.regexr.com)

__Step 1__ Match any character
```
.
```

__Step 2__ Match only the first character
```
^.
```

### Introduce quantifiers and show Regexr blurb
__Step 3__ Match strings that are 8-12 characters long. 
```
^.{8,12}$
```

__Step 4__ Remove upper range in our quantifier to specify a minimum length only.
```
^.{8,}$
```

### Basic intro to Capturing Groups, Character Sets, and Positive Lookaheads

- ### Character Sets allow us match any character between the square brackets []

__Step 5__ Add `a-z` character set.
```
^[a-z].{8,}$
```
This validates if the string is at least 8 characters long and starts with a lower case letter

- ### Capturing Groups () are used to group multiple Regex tokens together. This allows us to use Positive Lookahead which we're going to use to validate each of our our specific password requirements.

- ### Positive Lookahead (?=) Matches a group after the preceeding expression. In our case the preceeding expression is ^ or the beginning of our password string. We'll use the positive lookahead to check for lowercase letters at any position in our string. 

__Step 6__ Match strings with a length of 8 that contains at least 1 lower case letter.
```
^(?=.*[a-z]).{8,}$
```

__Step 7__ Illustrate case sensitivity by changing character set to `A-Z` in uppercase.
```
^(?=.*[A-Z]).{8,}$
```

__Step 8__ Re-add lowercase character set in an additional positive lookahead. We can see that our all lower case "password" is no longer matching. 
```
^(?=.*[A-Z])(?=.*[a-z]).{8,}$
```

__Step 9__ Add a positive lookahead for numbers `0-9`.
```
^(?=.*[A-Z])(?=.*[a-z])(?=.*[0-9]).{8,}$
```

__Step 10__ Now we'll add a capture group for special characters. Since many special characters mean specific things in Regex, we'll need to use a `\` to escape some of them. 
```
^(?=.*[A-Z])(?=.*[a-z])(?=.*[0-9])(?=.*[!@#\$%\^&\*_]).{8,}$
```
