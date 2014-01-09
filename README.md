ChurchServicePlanner
====================

CSP is a webapp for your Church to plan your Services!
This is the SOurce-Code for the WebApp hosted @ WebDaD.eu

# Legend
- + = Added
- - = Removed
- % = Changed (eg bugfix)
- ? = To be discussed

# MileStones

## 1 (Alpha) YYYY-MM-DD:
- [ ] Basic Framework
- [ ] UserManagement (Database Only)
- [ ] ChurchManagenent (Database Only)
- [ ] Module MusicTeams

## 2 (Beta) YYYY-MM-DD:
- [ ] Module Events
- [ ] Module Locations
- [ ] Module ServiceManager
- [ ] Module Preacher
- [ ] Module Technicians
- [ ] Module Songs
- [ ] Export to PDF
- [ ] Notification Mail to People

## 3 (Pre-Release) YYYY-MM-DD:
- [ ] Styling
- [ ] Module UserManagement
- [ ] Module ChurchManagement
- [ ] Export as SongBeamer
- [ ] Export as OpenLP
- [ ] Module-REST Combined as global REST
- [ ] robots.txt

## 4 (Release) YYYY-MM-DD:
- [ ] Connect to Google Drive (Save Data, Open Data)
- [ ] .htaccess Mod_Rewrite to allow nice RESTing

# Done

- + 2014-01-07: D: Filled Readme.md

# Modules

## Basic Framework
The Basic Framework allows for Loading of the Module via JavaScript.
It loads all Modules into the navigation and includes the javascript-files.
It also Displays the Next Event as featured and other Events to

Table:
t_modules: ID(P) | NAME | NAV_NAME | FOLDER | VERSION

## Module ChurchManagement
For CSP being a WebApp, multiple churches may use it.
So there will be a Table for churches and every DATA-Table will hold a Link to the church_id.

Table:
t_churches: ID(P) | NAME | LOGO | HOMEPAGE | MAIL | MAIN_USER

Forms:
Edit my Chruch Data.

A Chruch will be created if a User registers for no church.

## Module UserManagement
Everyone working with the WebApp must login as a User or register.
On registering you may create a new church or sign up to one. Then the main_user must accept you.

Table:
t_user: CHURCH_ID | ID(P) | NAME | VORNAME | LOGIN | MAIL | PWD

Forms:
Edit my Data.
Accept User for Church.
Delete Me.
Login/Logout.


## Module MusicTeams
This Module allows the Management of the MusicTeams.
A MusicTeam consists of users with an instrument and maybe a singing voice.

Table:
t_musicteams: CHURCH_ID | ID(P) | NAME | DESCRIPTION
t_musicteams_intruments : ID(P) | NAME | ICON | DESCRIPTION  <-- This is a global table like modules!
t_musicteam_has_users: CHURCH_ID | MUSICTEAM_ID(P) | USER_ID(P) | SINGS | INSTRUMENT_ID

Forms:
CRUD on musicteams
U allows to add/delete members


## Module Events
An Event is the MainUnit of the App.
It may be a Service, a Concert, ...
It Consists of MetaData and a RunDown.

RunDown-Items are having a TYPE, which changes the forms slightly
TYPES:
- Information
- Song
- Sermon
- Intro
- Outro
- Other
(More Types may be added as needed)

Table:
t_events: CHURCH_ID | ID(P) | EVENTDATETIME | NAME | DESCIRPTION | PREACHER_ID | SERVICEMANAGER_ID | MUSICTEAM_ID | LOCATION_ID
t_event_has_techs: CHURCH_ID | EVENT_ID(P) | USER_ID(P)
t_event_has_items: CHURCH_ID | EVENT_ID(P) | ID(P) | NAME | TYPE | DESCRIPTION | TYPE_DATA[maybe a attachment, songid, ...] | DURATION

Forms:
CRUD on events + edit rundown
U = MetaData and adding of techs
RunDown: CRUD Items


## Module Locations
This Module holds all Locations, where a Service may be hold.
Interesting for outdoor Events or wandering churches

Table:
t_locations: CHURCH_ID | ID(P) | NAME | DESCRIPTION | STREET | NR | PLZ | CITY | ADDITIONAL

Forms:
CRUD on locations

## Module ServiceManager
This MetaModule allows to set Users as ServiceManagers.

Table:
t_servicemanagers: CHURCH_ID | USER_ID(P)

Forms:
Add/Remove from List

## Module Preacher
This MetaModule allows to set Users as Preachers.

Table:
t_preachers: CHURCH_ID | USER_ID(P)

Forms:
Add/Remove from List

## Module Technicians
This MetaModule allows to set Users as Technicians.

Table:
t_techs: CHURCH_ID | USER_ID(P)

Forms:
Add/Remove from List

## Module Songs
Allows the Management of Songs.
A Songs consists of MetaData and SongParts.

Table:
t_songs: CHURCH_ID | ID(P) | NAME | SONGBOOK | VERSION | AUTHOR | COPYRIGHT | MELODY | CHRUCHSONGID
t_song_songparts: CHURCH_ID | ID(P) | SONG_ID | CONTENT | ORDER

Forms:
CRUD on Songs + Edit SongParts
U = Edit MEtaData
CRUD on Song-SongParts

## Notifications

People should get Note of Events, Changes, etc...
But How?

## Export

There are a number of options to Export the Data

### PDF
Every Module may offer Data-Export as PDF.

### SongBeamer
For a single Event, the Songs may be loaded as .sng-Files, the RunDown as .col-Files (with Songs and events/attachments). EveryThing will then be serves as zip-File.
Option will be if Songs Only or with Attachments and Data

### OpenLP
TODO

### Google Drive
TODO

## REST
The REST is modular.
To ensure only a valid user may see the data of his church only it uses HTTP Authentification.
Based on the login, the church_id will be used to filter results
Base Object is URL/REST/
After that, every module is an object, e.g. URL/REST/preacher
The objects are now GET-Only.

Customers that have a password may also login and see objects filtered to them.
e.g. URL/REST/events/list.html

"list" will be supported by every module and shows a list of object_ids

Returntypes are:
- html
- xml
- json

# Developers
- D: @DSigmund

# License
GNU GPL v2 (see LICENSE)
