1) Back in your Terminal window, make sure DataStax Enterprise is still running with ./dsetool status. If not, restart DataStax Enterprise.

########################

2) In the terminal window, start cqlsh:

/home/ubuntu/node/resources/cassandra/bin/cqlsh

########################

3) In cqlsh, create a keyspace called killrvideo. Use SimpleStrategy for the replication class with a replication factor of one.

CREATE KEYSPACE killrvideo WITH replication = {'class': 'SimpleStrategy', 'replication_factor': '1'} AND durable_writes = 'true';

########################

4) In cqlsh switch to the newly created keyspace with the USE command.

use killrvideo;
########################


5) Create a single table called videos with the same structure as shown above. video_id is the primary key.

CREATE TABLE videos(video_id text PRIMARY KEY ,added_date text,title text );
########################

6) Manually insert a single record using into the table using INSERT command. Use the first row from the table below:

INSERT INTO videos (video_id , added_date , title ) VALUES ( '1645ea59-14bd-11e5-a993-8138354b7e31','2014-01-29','Cassandra History');
########################

7) Write a SELECT statement to verify your record was inserted.

select * FROM videos ;
########################

8) Insert the second record as well and run a select statement to verify it's there.

INSERT INTO videos (video_id , added_date , title ) VALUES ( '245e8024-14bd-11e5-9743-8238356b7e32' , '2012-04-03' , 'Cassandra & SSDs' );
SELECT * FROM videos;
########################

9) Let's remove the data you inserted using the TRUNCATE command.

TRUNCATE videos;
########################

10) Execute the following command to import data into your videos table.

COPY videos(video_id, added_date, title) FROM '/home/ubuntu/labwork/data-files/videos.csv' WITH HEADER=TRUE;
########################

11) Use SELECT to verify the data loaded correctly.

SELECT * from videos;
########################

12) Use SELECT to COUNT(*) the number of imported rows. It should match the number of rows COPY reported as imported.
########################

13) To leave CQLSH execute this command:

QUIT


########################
########################
########################
videos.csv

video_id , added_title , title
1645ea59-14bd-11e5-a993-8138354b7e31 , 2014-01-29 , Cassandra History
245e8024-14bd-11e5-9743-8238356b7e32 , 2012-04-03 , Cassandra & SSDs
########################
