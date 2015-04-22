---
layout: post
title: "python regular expression"
date: 2014-10-03 13:00:03 -0400
comments: true
categories: python
---

###regular expression
- use the match string
	- but not all the string can be matched
<!--more-->
###basic character in python 
```
import re
```
- ordinary character
    - like re'test' will match the string test
- oral character 
    - like . ^ $ * + ? {} [] \ | ()
    - like []
        - use to direct to a range of the string set
        - ```
        s = r'abc'
        re.findall(s, "aaaaaaaabc")
        //use []
        rt = "top tip tap twp tep"
        r1 = r"t[io]p"
        re.findall(r1, rt)
        //output ['top'], ['tip']
        r2 = r"t[^io]p"
        re.findall(r2, rt)
        //output ['tap'],['tep'], ['twp']
        ```
        - and oral character is no use in the []
        - also can use `r'0-3'` replace `r'0123'`
            - use 'r'[0-3a-cA-C]'' replace `r'[0123abcABC]'`
    - like ^
        - use the match the head of the line
        - ```
        s = r'^t'
        st = 'tss'
        //output ['t']
        ```
    - like $
        - use to match the end of the line
    - like \
        - used if you want to transform the oral character into a original one
        - use '\^' to make ^ as a original character
        - and can be used as
            - \d match [0-9]
            - \D match [^0-9]
            - \s match [\t\n\r\f\v] 
                - means and empty character
            - \S match [^\t\n\r\f\v] 
                - means non empty character
            - \w match [a-zA-Z0-9]
            - \W match [^a-zA-Z0-9]
    - like *
        - match multiple character
        - means repeat the character in front of the * for 0-many times
        - ```
        r = r'ab*'
        rt = 'abbbbbb'
        re.findall(r, rt)
        //output['abbbbbb']
        ```
    - like +
        - match the charter that appear more than one time
    - like ?
        -  match the charter that appear zero or one time
        - can be used as minimum match
            - `r = r'ab+?'`
            - `rt = 'abbbbbb'`
            - output the ab
    - like the {}
        - means that the character can be repeat how many times
        - ```
        r = r'a{1,3}'
        rt = 'aaaaa'
        then can match a, aa, aaa
        ``` 
        - {0,} == *
        - {1,} == +
        - {0,1} == ?
        
        
###functions
- compile the expression to speed up
    - ```
    r = r'\d{3,4}-?\d{8}'
    p_telephone = re.compile(r)
    p_telephone.findall('010-12345678')
    //output ['010-12345678']
    ```
    - and you can add attribute while compile
- there are some normal functions
    - match
        - only search from the front
        - ```
        p_telephone.match('o010-12345678')
        //output nothing because the 010-12345678 is not start from the begin
        ```
    - search
        - search the whole string
        - no matter where the number is , if you can find it, you can find it.
    - findall
    - finditer
        - the same as findall but you need to use iter so that you can get the value
        
- and there are sub(), subn(), split()
    - sub()
        - ```
        r = r'c..t'
        re.sub(r, 'aaa', 'caat cast cccc')
        //output 'aaa aaa cccc'
        ```
    - subn()
        - the difference between sub and subj is that subj provide a count of the how many stuff you replace
        - ```
        r = r'c..t'
        re.subn(r, 'aaa', 'caat cast cccc')
        //output 'aaa aaa cccc', 2
        ```
    - split()
        - split the string using a regular express
        - ```
        re.split(r'[\+\*\-]', '1+2-3*5')
        //output ['1', '2', '3', '5']
        ``` 
    - use `dir(re)` to see what functions re have

###flags in re module
flags |meaning
----|-----
dotall, S| let . match all the character contains \n
ignore case, I |make the match no sensitive about the uppercase and lowercase
locale, L | do locale-aware match, match the French or the other language
multiline, M | match multiline, affect ^ and $
verbose, X | can use the REs verbose status, and make the organise more clearly

###devision
- ()
- `email = r'\w{3}@\w+(\.com|\.cn)'`
- use the () to divide the .com and .cn
- so that we can use the regular form to match email address

        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        
        













