# my_ds_babel
Introduction
Data is heart of an information system. Converting them from a format to another or migrating them to another database is a very important skills.

It would be great if every information system were able to speak the same language...

Tower of Babel

Your mission will be to help translate from one format to another.

We will be working with 2 very popular format: SQL and CSV.

What is SQL?
It stands for Structured Query Language.
It helps you perform query into a database. Query will have the format of:

SELECT (GET)
INSERT
UPDATE
DELETE
It has a very specific syntax:

SELECT * FROM table;
INSERT INTO table_name(id, name) VALUES(1, 'Pacific Ocean');
UPDATE ...
DELETE ...
How to connect to a sqlite databse?
Good question, google might have an answer. :-)

What is CSV?
It stands for Comma Separated Values
There are files, with multiple line and column. Divider are , (comma) and new line (\n)

id,name
1,Pacific Ocean
2,Atlantic Ocean
3,Indian Ocean
4,Artic Ocean
5,Southern Ocean
Interesting fact: the Southern Ocean has been recognized by the International Hydrographic Organization in 2000. It borders Antarctica in its entirety. wiki link

Example in ruby:

require "sqlite3"
require 'csv'

db = SQLite3::Database.new "volcanos.db"

# Create a database
rows = db.execute <<-SQL
  create table volcanos (
    volcano_name varchar(100),
    latitude int,
    .... OTHER FIELDS
  );
SQL

csv = File.read('list_volcano.csv')

CSV.parse(csv, headers: true) do |row|
    db.execute "insert into volcanos values ( ?, ?, ?, ?, ?, ? )", row.fields
end

p db.execute( "select * from volcanos" )
Part I SQLtoCSV.
We will start with the SQL format to CSV

Your function will receives a connection (an sqlite3 object from import sqlite3 which will be already connected), table_name.
Your function will transform the content of table_name to CSV format and return it. (Columns separated by comma and rows separated by \n)

Part II CSVtoSQL
Your function will transform the content to SQL format by creating and the table_name and adding each rows to it.

Part III
a) You will use your function in order to convert the list of all volcanos from CSV to SQL.

b) You will use your function in order to convert the list of all fault lines from SQL to CSV.
Data are inside the table named: fault_lines.

Technical specifications
Write a class with two classmethod which convert a format to another. (Part I and Part II)

You are free on the implementation on how to connect to the database and which arguments to send to your functions.

Your code will be here to show to your reviewer your implementation, but we are looking for the 2 results files. ;-)
Your submit files will be: all_fault_lines.csv and list_volcanos.db (table volcanos).
