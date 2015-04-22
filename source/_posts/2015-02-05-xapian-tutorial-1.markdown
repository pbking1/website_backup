---
layout: post
title: "xapian_tutorial_1"
date: 2015-02-05 16:40:48 -0500
comments: true
categories: search_engine c++

---

- note:some of the content and code are refer from http://www.coder4.com/archives/2218

###basic index build and search
- first of all, xapian is an open source c++ search engine.
- also note that xapian is called "Zap-in"
<!--more-->
####basic data structure
- used for search
    - `Xapian::Database` 
        - used to read index
    - `Xapian::Enquire`
        - use with Database
        - use to search
    - `Xapian::QueryParser`
        - query sentence parser
    - `Xapian::Query`
        - query
    - `Xapian::MSet`
        - the result set returned by searching
- used for build index
    - `Xapian::WritableDatabase`
        - use for built index
    - `Xapian::TermGenerator`
        - use for cut sentence, build index.
- for both
    - `Xapian::Document`
        - abstract of document
     - `Xapian::SimpleStopper`
         - the word used for ending
     - `Xapian::Error`
         - exception
         - use get_description() to get detailed info.
         
         
####how to build index
- open a `Xapian::WritableDatabase`
- Then prepare for the document
    - use `set_data(string)` to set data(only one)
    - use `add_value(slot, string)` to set field(can have more), slot can not be -1
    - these two method is only used for storage
        - not used for parse or index
- build index field
    - use `Document.add_term(word, pos)`
    - use `Xapian::TermGenerator` and `.set_document(doc)`
        - then pass the string using delimiter space into index_text
        - then the doc will have the index field of this document
- after building the document, import into database
- use DB.commit()


####how to query
- open `Xapian::Database`, the path is the same as WriteableDatabase
- use DB to construct `Xapian::Enquire`
- use `Xapian::QueryParser` to parse the string and generate `Xapian::Query`
- use `enquire.set_query()` to query
- get the result set by using `enquire.get_mset(start, len)`.
- use `Xapian::MsetIterator` to traverse the MSet. 
    - use `get_rank()` to get the rank
    - use `get_document` to get the document
   
####query grammer
- `Term | Term | Term`
- `Term -> Term ~ Term`
    - `~` is used for similar word

####About field
- When building index
    - use `Xapian::TermGenerator` for example
        - we need to set the `TermGenerator.set_database(db)`
        - when building the index field
            - `index_text(text, wdf_inc=1, prefix)`
                - The second and third parameter are default
                - The second is TF increase
                - The third is prefix
    - When query
        - add mapping using `Xapian::QueryParser`
        - `.add_prefix("title", "T")`
        - Then the `qp.parse_query` can have field when query the string
        - for example
            - 'title:news AND content:basketball'
            - and now there are two field
                
         
####sample code
 
- create_index.cpp
```
 	#include<xapian.h>
	#include<iostream>
	#include<string>
	using namespace std;

	#define CONTENT "70:69， This is man basketball race history the smallest point difference race ， smile to last is east man Chinese 。 Which can be said ， This time is the most famous victory and can be said this is the most lucky resuly 。After the end of the game, the coach of the Chinese aa and The boss bb hang togetherm and the two guy are so happy that the chinese win。"

	#define TITLE "This is a news"

	#define INDEX_PATH "./index_data"

	#define F_DOCID 1

	int main(int argc, char *argv[]){
		try{
			//The text to be indexed
			string content(CONTENT);
			string title(TITLE);

			//open a database and write
			Xapian::WritableDatabase db(string(INDEX_PATH), Xapian::DB_CREATE_OR_OPEN);
			
			//term generator
			Xapian::TermGenerator indexer;

			//Make document
			Xapian::Document doc;
			doc.add_value(F_DOCID, string("1104"));
			doc.set_data(content);
			indexer.set_document(doc);
			indexer.index_text(title, 1, "T");
			indexer.index_text(content, 1, "C");

			//add document to db
			db.add_document(doc);

			//flush to disk
			db.commit();

		}catch(const Xapian::Error &e){
			cout<<e.get_description()<<endl;
		}
		return 0;
	}

```
 
- search.cpp
```
	#include<xapian.h>
	#include<iostream>
	#include<string>
	using namespace std;
	#define QUERY "title:news AND content:70"
	#define INDEX_PATH "./index_data"
	#define F_DOCID 1
	int main(){
		try{
			//The string for query
			string query_str(QUERY);

			//open the database
			Xapian::Database db(string(INDEX_PATH));

			//open search handle
			Xapian::Enquire enquire(db);

			//Parser Query
			Xapian::QueryParser qp;
			qp.add_prefix("title", "T");
			qp.add_prefix("content", "C");
			Xapian::Query query = qp.parse_query(query_str);
			cout<<"Query is "<<query.get_description()<<endl;

			//find the top 10 result
			enquire.set_query(query);
			Xapian::MSet result = enquire.get_mset(0,10);
			cout<<result.get_matches_estimated()<<" result found"<<endl;

			//print the result
			for(Xapian::MSetIterator iter = result.begin(); iter != result.end(); iter++){
				Xapian::Document doc = iter.get_document();
				cout<<iter.get_rank()<<": docid "<<doc.get_value(F_DOCID)<<", data"<<doc.get_data()<<endl;
			}

		}catch(const Xapian::Error e){
			cout<<e.get_description()<<endl;
		}
		return 0;
	}

```        
         
         
         
         
         
         
         
         
         
         
         
         
         
         
         
         
         
         
         
         
         
         
         
         
         
         
         
         
         
         
         
         