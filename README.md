Concept 
-------

**Existing**: 
- I have a mailing list among university classmates where I occasionally (once a week) send people resumes 
(as attached Word/pdf files), among other messages. 
- The mailing list in newsletter style, powered  by GNU Mailman.

**Target**: I want to keep a repository of these files and send out a listing of recent resumes to subscribers 
or redirect subscribers to a webpage with such listing. 

**Motivation**: 
- people send out some resumes of their friends/relatives, but immediate interest/response
is quite low 
- having a listing of resumes 'in active search' (or passive, actually) may serve to more people finding jobs 

Design
------
Components needed :

1. file storage (AWS S3 or NoSQL database)
2. file placement procedure (ideally an additional mailing address <resume@mymailinglist.com>, 
  which adds message body anа attahcments to database)
3. editing/categorising on resumes by admin on a separate web page or a set of config files or both
  (assign an industry of job, job level, other categories/flags or parameters)
4. a  frontpage of current resumes with authorisation, that I can possibly send as body of e-mail message
5. a database of mailing list subscribers 

User scenarios
--------------

**Participants**:

People:
 - Endorser (E) - a mailing list subscriber who sends a resume
 - Resume Person (RP) - a person who's name is actualy on a resume 
 - Subscribers(Subs) - a mailing list subscriber 
 - Admin(A) - a mailing list God in need of more tools to satisfy the constituents Subscribers
 
Machines:
 - List: mailing list, served by GNU Mailmain  
 - Bot: e-mail bot to handle messages with resumes
 
Content:
 - Msg: e-mail message
 - Resume Listing (Listing) - a page with a list of resumes
 
**Worklow**:

Prelude:
- E talks to A: *"hey, got a this chaps' resume, why not send it to the list?"*
- A: *"OK, please tell me what this lil' bastard wants and give me the resume file"*
- E sends email Msg to A with some text about RP and resume file(s) in attachment

Current:
- A sends Msg to List 
- Subs glance at Msg
- Msg is forgotten next day, nothing happens

Target:
- A sends Msg to Bot and List 
- Bot:
  - extracts Msg text and attachments into database fields
  - allows Admin to edit fields
  - prepairs a listing of recent resumes
- A or Bot (or Bot at command of A) sends resume listing to List at end of week (or Wednesday)
- Subs read the listing: *"Ahh! Here are is that lil' bastard resume I noticed a week ago. Why not send it to our HR    department, they have a new opening."*
- RP gets hired to a new great job, everyone is happy

Clean up:
- some feedback loop to see what happened to a resume
- depreciation procedure to put resume off the list


TODO
---- 

I want someone to describe this requirement/design in more detail, that will be ready to 
give to individual developpers. Specifically I need:

  a) refine concept above    
  b) go over and seggest clarifications to user scenarios descriptions above  
  c) propos design in section above (building blocks and functionalities)  
  d) give advice/options for implementation  in design section (like file storage: AWS, Mongo)  

Comments:
 - in all of the above better separate basic functionality / additions - this is highly appreciated. 
 - Python microframeworks are preffered choice (eg Flask)
 - strictly no WordPress-like solutions 
