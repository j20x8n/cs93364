java c
Assignment Three: Database
Released: 20th   November 2024
Due: 23:59,   18th   December 2024
Synopsis:
You are going to store and manipulate some   data in aMongoDB   database. The   data   are related   to events and locations, similar to the suggested   dataset   in   our project.Problem 7E and Problem 8E are compulsory questions for ESTR   students.   For   CSCI   students,   you may   also   attempt these   questions.   However, we will   only   give you   feedback   without   any   extra   scores.
Environment setup:
Please follow lab08 to setup a   basic web server   using   Node.js and Express.   Also, please follow   lab09 to   setup   aMongoDB   database   and   access   it   using   Mongoose   in   Node.js.
Problem   1: Database Schema (20%)
Schema and Model in Mongoose help to confine   the   types   of   data   to be   stored. Your task   is   to   setup   two   Schemas:
1.       Event:
a.       eventId: number, required, unique
b.       name: string, required
c.       loc:   ObjectID ->   location documents*
d.       quota: number
2.       Location:
a.       locId: nmuber, required, unique
b.       name: string, required
c.         quota: number
*Remarks: Try to   accommodate the reference to   documents   in the   location   collection.   Check   Lecture   17 MongoDB from the Blackboard.
Problem 2: GET   (15%)
Your Express server should respond to this request:   GEThttp://server-address/ev/eventIDWhen   the   server   receives   this   request,   look   up   the   event   with   the   given   event   ID   from   the   database. Then print the event name, location   ID, location name, event quota on separate lines,   as   shown   in   the   illustration   below.   The   location   quota   is   not   necessary. All   field   names   and   string      values      should      be      quoted      with      double      quotes.      Extra      spacing      is      allowed,      and   brackets/commas do not need to be in separate lines.If   the given event ID is not found, output an understandable message in the response body with   status    code    404.   All   the   response    should    be    sent    as    HTTP   responses    with    content    type   text/plain.
   
Problem 3: POST (15%)
Your Express server should respond to this request:   POSThttp://server-address/evWhen   the   server   receives   this   request,   it   should   use   the   parameters   submitted   in   the   HTTP   request body to create a new event in the database.   A simple HTML form. like lab8_task2.html   in Blackboard can be used.However,   instead   of   letting   the   user   decide   the   event   ID,   your   code   should   assign   a   new   maximum event ID by looking into the database.   For   example,   if   123   is   the   current   maximum   event ID, the new event ID would be   124.Modify the form   so that it asks the user   for the   location   ID. A lookup should   be   done   to   check   if   the location quota is larger than or equal to the   new   event   quota.   If   not, the   event   should   not be created, and an error message should be responded to the user with status code 406.   (Note:   There is no need to check other event at the   same   location.)
If   the event is created successfully, respond to the user with the URL of   the created   event.   Use   HTTP status code 201.
Problem 4: DELETE (10%)
We allow users to delete an event using   this   request:   DELETE   http://server-address/ev/eventIDIf   the event ID is found, the event should be   removed   from   the   database.   Send   a response   with   status   code   204,   and   nothing   in   the   body.   If not   found,   show   a   simple   error   message   in   the   body with status code   404.
Problem 5: Some more   queries   (20%)
The following four requests need to   be handled:   Q1: GEThttp://server-address/ev
List all the events available, with details formatted   similar to the   illustration below.

Q2: GEThttp://server-address/lo/locatoinID
Show   the   details   for this   location   ID,   with   details   formatted   similar   to   the   illustration below.   Respond with an error message if   the location ID is not   found with   the   status   code   404.
   
Q3: GEThttp://server-address/lo
List all location available.   Show details similarly to the   illustration   in   Q1.
Q4: GEThttp://server-address/ev?q=number
List   all   the   events   with   enough   quota,   with   a   similar   format   in   Q1.   Respond   with   an   empty   array   if   there   is   none.
Problem 6: Updating with PUT (20%)
Implement a simple HTML user interface for updating event information. Assume that the   user always types in an existing event ID to   load   the   event  代 写Assignment Three: DatabaseJava
代做程序编程语言 information.   The   current   data   from   the database should be shown to the user, so that they   can   decide   what   to   edit,   in   an   HTML   form. Then, update the database with the user data on submission, using this request:
PUThttp://server-address/ev/eventIDThe event should always be updated successfully. Respond to the user with the updated   event      details as in Problem   1. You may combine this HTML form. with   the POST form   in   Problem   3   or create a new HTML file. Checking of   event and location   quota   is not   necessary   here.
Problem 7E: Counting GET   (15%)
In every GET queries in this assignment, add   an   extra   field   “query_no”, which   indicates   the   total count of   GET queries for this user on this browser including requests giving   errors.
Show it only in the response when there is no error. The   count   should be   reset   if   there   is   no   further query in   5 minutes.Q1: Perform   GET   http://server-address/ev/1   (or   any   other   GET   operations)   for   several   times       and show the details for this response with “query_no” larger than   1   similar to   the   illustration   below.
   
Q2: GEThttp://server-address/ev/1   (or any other GET operations) after   5   minutes   and   show the details for this response with “query_no” equal to   1   similar to the   illustration below.
   
Problem 8E: GraphQL GET (20%)You are required to transform. all GET operations in this assignment into a GraphQL   API using   Apollo   Server   while   maintaining   the   same   underlying   data   model   and   business   logic. After   starting             the                server                with             node                server_graphql.js                command,                navigate             to   http://localhost:3000/graphql   in your browser.
You   can   query   all   locations   and   events,   and your response   should be   similar to   the   examples   below:
   
Formats and assumptions:
Please pay attention for the followings:
1.       In   this   assignment,   since   the   response body   do   not   always   confirm   to   standard   JSON   formats,   e.g.,   for   error   messages,   please   always   use   text/plain   as   the   Content-   Type.
2.       The      JSON-like      objects      and      arrays       should      be      readable      by      standard      JavaScript   JSON.parse() if   all   newline   characters   are   removed.
3.       Use the   CORS middleware   for   express to   enable   submission   from   local HTML   forms   (more details in lab08).
4.       Unless   otherwise   specified,   the   HTTP   status   code   should   be   200   OK   by   default.   201   Created   is used   for responding to   successful   POST requests,   and   204   No   Content   is   used for responding to successful DELETE requests.
5.       For   development,   you   may   feel   free   to   populate   your   database   with   testing   data   (i.e.,   create   your   own   fake   data   for   testing).   Please   create   a   folder   named   database_setup.   You can create database whose name is   assignment3   and   create two   collections   which   are   locations   and   events.   In   the   locations   collection,   please   import   from   JSON   file   database_setup/assignment3.locations.json.   In   the   events   collection,   please   import   from JSON database_setup/assignment3.events.json.
6.       For   grading,   graders   will   use   another   set   of data   in   their   database.   Hence,   you   code   should be   adaptive to   different   data. Assume that   there   is   always   at   least   one   location   and one event in the database when grading   (i.e.,   it will   not   be   an   empty   database).   All   locations linked from events   are valid   in the   database.
7.       Assume that the   input   data type   is   always   correct,   i.e.,   only numbers   will   be   input   for   number fields.   All numbers are positive numbers. When grading, no fields   are blank.
8.       Assume   that   user   always   enters   a   valid   and   existing   location   ID   when   creating   or   updating events.
9.       Unless otherwise specified, events or locations with missing   quota   will not be tested.
10. The    Node    server    should      start      at    port      3000.    Assume    the      access    URL      starts      with   http://localhost:3000.
11. There are   no cosmetic requirements for this assignment.   You are welcome to implement   extra styles and features   at your   own   ability.
12.   Your   submission   should contain   only   one JavaScript   file   (one more JavaScript   file   for   Problem   8E).



         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
