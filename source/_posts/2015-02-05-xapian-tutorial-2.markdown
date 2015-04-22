---
layout: post
title: "xapian_tutorial_2"
date: 2015-02-05 19:54:20 -0500
comments: true
categories: search_engine c++

---

###The expand of synonym(同义词)
- such as ‘I love you‘ and 'ILU'
- process to do this
    - Write the synonym into database
        - use `WriteDatabase::add_synonym(term,synonym)`
        - but we can only do 'I love you' -> 'ILU'
            - if we want to reverse it, we need to add the reverse version

###use the synonym when query
- use `QueryParser::set_database()` to set db
- when using the `QueryParser::set_database()`, the second parameter use `FLAG_SYNONYM` or `FLAG_AUTO_SYNONYMS`
- `FLAG_SYNONYM` is the ~WORD format in the query sentence. expend the synonym of the word automatically
- `FLAG_AUTO_SYNONYMS` is expend all the phrase, do not need to write ~
<!--more-->
###sample

- makefile
    - 
```

    all:
	    g++ -o index -I/usr/local/include -l xapian index.cpp
	    g++ -o query -I/usr/local/include -l xapian query.cpp
    clean:
    	rm -rf index index_data/ query
```

- index.cpp

```
     #include<xapian.h>
     #include<iostream>
     #include<string>
     using namespace std;
     #define CONTENT "70:69， I love you This is man basketball race history the smallest point difference race ， smile to last is east man Chinese 。 Which can be said ， This time is the most famous victory and can be said this is the most lucky resuly 。After the end of the game, the coach of the Chinese aa and The boss bb hang togetherm and the two guy are so happy that the chinese win。"
     #define INDEX_PATH "./index_data"
     #define WORD1 "I love you"
     #define WORD2 "ILU"
    int main(int argc, char *argv[]){
	try{
		//The text to be indexed
		string content(CONTENT);

		//open a database and write
		Xapian::WritableDatabase db(string(INDEX_PATH), Xapian::DB_CREATE_OR_OPEN);
		
		//term generator
		Xapian::TermGenerator indexer;

		//add synonym
		db.add_synonym(string(WORD1), string(WORD2));

		//Make document
		Xapian::Document doc;
		doc.set_data(content);
		indexer.set_document(doc);
		indexer.index_text(content);

		//add document to db
		db.add_document(doc);

		//flush to disk
		db.commit();

	}catch(const Xapian::Error &e){
		cout<<e.get_description()<<endl;
	}
	return 0;}
```

- query.cpp

```
     #include<xapian.h>
     #include<iostream>
     #include<string>
    using namespace std;
     #define QUERY "~ILU AND Chinese"
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
		qp.set_database(db);
		Xapian::Query query = qp.parse_query(query_str, Xapian::QueryParser::FLAG_SYNONYM);
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