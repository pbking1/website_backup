---
layout: post
title: "xapian_tutorial_3"
date: 2015-02-06 02:50:50 -0500
comments: true
categories: search_engine c++

---

####filter
- There is a `faceted Search`, which is to preview the result of the query in many category. 
    - like if we search for 'apple'
        - the result may be classified into two
            - one is apple fruit
            - one is apple company
- actually, this is a filter.
    - we can classify before index, and store into index
    - and use value to filter them when query
<!--more-->
####how to build filter value
- use `Document::add_value`

####how to use filter when query
- two ways
    - one is use `Xapian::MatchDecider`, this return a bool value.
        - or we can use `Xapian::ValueSetMatchDecider`
            - `Xapian::ValueSetMatchDecider(slot, inclusive)`
                - slot means which slot to filter
                - inclusive means using filter or reduce
            - use `Xapian::ValueSetMatchDecider::add_value(string)` 
                - user can decide one or many set of value
                    - when document belong to one of these value
                        - make it filter or stay    
    - use `MatchSpy`
         


