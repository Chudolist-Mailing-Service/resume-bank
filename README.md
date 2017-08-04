TODO:
-----

- [ ] indicate weak point/ambiguitites in user scenarios (0.5-1h)
- [ ] outline your design in section 2 (1-1.5h) with focus on:
  - [ ] list and describe building blocks and functionalities
  - [ ] advice/options for implementation by block (like file storage: S3, Mongo)  
  - [ ] how would you test each block

1  Concept (not to edit)
------------------------

### Existing situation

- I have a mailing list among university classmates where I occasionally (once a week) send people resumes 
(as attached Word/pdf files), among other messages. 
- The mailing list in newsletter style, powered  by GNU Mailman.
- Immediate interest/response for resumes in mailing list is quite low

### Target functionality

Listing of resumes 'in active search' will help people find  more jobs: 

 - Keep a repository of resume files and supporting information 
 - Send out a listing of recent resumes to subscribers or redirect subscribers to a webpage with such listing. 


2  Design (to edit/rewrite)
---------------------------

Components needed :

1. file storage (AWS S3 or NoSQL database)
2. file placement procedure (ideally an additional mailing address <resume@mymailinglist.com>, 
  which adds message body anа attahcments to database)
3. editing/categorising on resumes by admin on a separate web page or a set of config files or both
  (assign an industry of job, job level, other categories/flags or parameters)
4. a frontpage of current resumes with authorisation
   - a frontpage must also fit as email message body
5. a database of mailing list subscribers 

Design solutions:

database (emails, files, people):
  - mongodb

framework:
  - flask

admin page:
  - bootstrap for design, python django framework and mongodb and digital ocean for cloud hosting

hosting:
  - ec2/ digital ocean 
  - AWS services?


3 User scenarios (to comment/refine)
------------------------------------

### Participants:

**People**:
 - Endorser (E) - a mailing list subscriber who proposes to send a resume
 - Person (P) - a person who's name is actualy on a resume 
 - Subscribers (Subs) - a mailing list subscriber 
 - Admin (A) - a mailing list maintainer in need of more tools to satisfy Subscribers
 
**Machines**:
 - List: mailing list, served by GNU Mailmain (hosted at EC2) 
 - Bot: e-mail bot to handle messages with resumes (hosted elsewhere on AWS) with address <resume@mymailinglist.com> 
 
**Content**:
 - Msg: e-mail message
 - Resume Listing (Listing) - a page with a list of resumes
 
### Worklow:

##### Prelude:
- E talks to A: *"hey, got a this chaps' resume, why not send it to the list?"*
- A: *"OK, please tell me what this lil' bastard wants and give me his resume file"*
- E sends email Msg to A with some text about P and resume file(s) in attachment

##### Current flow:
- A sends Msg to List 
- Subs glance at Msg
- Msg is forgotten next day, nothing happens

##### Target flow:
- Admin sends Msg to List and to Bot
- Bot:
  - extracts Msg text and attachments into database fields
  - allows Admin to edit fields
  - prepairs a listing of recent resumes
- Admin sends resume listing to maining list at end of week (or Wednesday)
  - as link to listing page
  - inside message body
- Subs read the listing: 

  > "Ahh! Here are is that lil' bastard resume I noticed a week ago. 
  > Why not send it to our HR  department, they have a new  opening."
  
- P gets hired to a new great job, everyone is happy

##### Clean up:
- some feedback loop to see what happened to a resume
- depreciation procedure to put resume off the list


4 Add-ons
----------

#### Bot send e-mail itself to list

send out e-mail:
- mail chimp
- sendgrid
- other?


