TODO:
-----

- [ ] indicate weak point/ambiguitites in user scenarios (0.5-1h)
- [ ] outline your design in section 2 (1-1.5h) with focus on:
  - [ ] list and describe building blocks and functionalities
  - [ ] advice/options for implementation by block (like file storage: S3, Mongo)  
  - [ ] how would you test each block

1  Concept 
----------

### Existing situation

- I have a mailing list among university classmates where I occasionally (once a week) send people resumes 
(as attached Word/pdf files), among other messages. 
- The mailing list in newsletter style, powered  by GNU Mailman.
- Immediate interest/response for resumes in mailing list is quite low, listing of resumes 'in active search' will help people find  more jobs: 

### Target functionality

 - Keep a repository of resume files and supporting information 
 - Send out a listing of recent resumes to subscribers or redirect subscribers to a webpage with such listing. 


2  Design
---------

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


3 User scenarios 
----------------

### Participants:

People:
 - Endorser (E) - a mailing list subscriber who proposes to send a resume
 - Person (P) - a person who's name is actualy on a resume 
 - Subscribers (Subs) - a mailing list subscriber 
 - Admin (A) - a mailing list maintainer in need of more tools to satisfy Subscribers
 
Machines:
 - List: mailing list, served by GNU Mailmain (hosted at EC2) 
 - Bot: e-mail bot to handle messages with resumes (hosted elsewhere on AWS) with address <resume@site.com> 
 
Content:
 - Msg: e-mail message
 - Resume Listing (Listing) - a page with a list of resumes
 
### Worklow:

- [x] marks e-mail bot functionality

Before bot: 
- [ ] Endorser talks to Admin: *"please send this resume to mailing list"*
- [ ] Admin: *"OK, tell me what the guy wants and send me his resume file ()"*
- [ ] Endorser sends email Msg to A with some text about Person and resume file in attachment
- [ ] Admin sends email Msg to List and to Bot
- [ ] GNU Mailman/PostFIX sends email Msg to List 

An e-mail bot:
  - [x] accepts e-mail at <resume@site.com> (todo: what program does this and how? - describe in detail) 
  - [x] extracts Msg text and attachments into database fields (this is AWS lamdba)
  - [x] provides Admin with admin page to edit fields (this is flask)
  - [x] provides Admin with a listing of recent resumes at stable URL (this is flask)

Admin (this can be later changed to bot functionality a bot can send a message- not todo now):
  - [ ] manually copy-pastes a link to listing
  - [ ] sends it to mailing list manually 

Subscribers:
  - [ ] Subscriber goes to a listing page
  - [x] Sub authenticates at listing page
  - [x] Sub browses the job listings

- [ ] Person gets hired to a new great job, everyone is happy

##### Clean up:
- some feedback loop to see what happened to a resume
- depreciation procedure to put resume off the list


4 Add-ons
----------

Bot send e-mail itself to list:
- prepare html contents for message

Send out e-mail:
- mail chimp
- sendgrid
- other?
