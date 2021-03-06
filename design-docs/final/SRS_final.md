 <div align=center>
   <h1>Software Requirements Specification</h1>
   <h2>Project Recommend</h2>
   <b> Music Recommendation System </b><br />
   <b> Version <i>1.0</i></b>
</div><br /><br />


#### Team Project Recommend

- **Surajnath Sidh**  U101114FCS146
- **Rajdeep Mukherjee**  U101114FCS115
- **Raghav Mittal**  U101114FCS111
- **Pranshu Sahijwani**  U101114FCS104
- **S. Shakthi**  U101114FCS196
- **Saumya Gupta**  U101114FCS126

#### NIIT University
##### 18-Sep-2016

<hr/><br />

# Table of contents
1. [Introduction](#introduction)  
1.1 [Purpose](#introduction-purpose)  
1.2 [Document Conventions](#introduction-dc)  
1.3 [Intended Audience and Reading Suggestions](#introduction-iars)   
1.4 [Product Scope](#introduction-product-scope)  
1.5 [References](#introduction-references)  
1.6 [Terminology](#introduction-terminology)
2. [Overall Description](#od)  
2.1 [Product Perspective](#od-pp)  
2.2 [Product Functions](#od-pf)  
2.3 [User Classes and Characteristics](#od-ucc)  
2.4 [Operating System](#od-os)  
2.5 [Design and Implementation Constraints](#od-di)  
3. [External Interface Requirements](#eir)  
3.1 [User Interfaces](#eir-ui)  
3.2 [Hardware Interfaces](#eir-hi)  
3.3 [Software Interfaces](#eir-si)  
3.4 [Communications Interfaces](#eir-ci)  
4. [System Features](#sf)  
5. [Other Nonfunctional Requirements](#onr)
6. [Other Requirements](#otherreq)  
[_Appendix_](#appendix)  
<hr />  


##### Product : Project Recommend
##### Description : An offline music recommendation system
##### Status : Waiting for Review
##### Development Status  : design phase

----

## Revisions

#### Latest
    Current Version : 1.0
    Current Status : Work in Progress
    Date : 18-09-2016

### Revision History
- Version 1.0
    - Date : 18-09-2016
    - Reason For Changes : initial changes



# 1. Introduction <a name="introduction"></a>
## 1.1 Purpose <a name="introduction-purpose"></a>
The purpose of this document is to provide a debriefed view of requirements and specifications of the project called "Project Recommend".

Goal of this project is to provide recommendation on your offline music collection that you have
in your computer locally.

This document discusses about whole system from backend to user interactions.

The tools used in this project are described in this
document as follows :

- Libraries used for back end control of application
- Libraries used for UI and UX design of the application
- Database used for music referencing
- Classifiers used for classifying data and yielding recommendations


## 1.2 Document Conventions <a name="introduction-dc"></a>
- All terms are in italics style.
- Main features or important terms are in bold style.
- TBD means "To be Decided", these are the components that are not yet decided
- For more references see [Terminology](#introduction-terminology).

## 1.3 Intended Audience and Reading Suggestions <a name="introduction-iars"></a>
- Anyone with some basic knowledge of programming can understand this document. The document is intended for Developers, Software architects, Testers, Project managers and Documentation Writers.
But anyone with programming background and some experience with UML can understand this document.

- It is divided into 5 phases with sections 3, 4, 5 being intended for developers and software managers but other sections can be understood by anyone having little knowledge about software.

This Software Requirement Specification also includes:

- Overall description of the product
- External interface requirements
- System Features
- Other non functional requirements


## 1.4 Product Scope <a name="introduction-product-scope"></a>

- Offline Music Recommendation is an area of application development that is yet to be fully explored as there has not been enough attempts to develop a software to fulfil this need. Browsing over the internet one may get enough music recommenders online but that is the real catch here, they are mostly **_online_**. Here our development team is trying to build an **_offline_** music recommender application to fulfil users need of getting music suggestions based on their already present music collection.

- Offline Music recommendation will involve recommendation of familiar tracks and familiar genres of music available both on the internet and from offline library

- Name of the project is "Project Recommend". It is a Desktop App.
- It plays music and provides suggestions based on track which user is listening to from both offline library which is available in user's machine as well as on internet.

##### Advantages
- It provides suggestions from local music library.
- Works with slower internet connection because it needs less bandwidth for providing recommendations.
- It uses [MusicBrainz][musicbrainz-website] database for getting metadata of all the music present in user's local library and recommend tracks.
- it is not platform or service specific
- it is not bounded with any music provider services so it is suggestions are not limited to particular service
- There are no specific audience for this software. Anyone can install it and use it.

## 1.5 References <a name="introduction-references"></a>
- This document is written in github flavored Markdown.

- IEEE. IEEE Std 830-1998 IEEE Recommended Practice for Software Requirements Specifications. IEEE Computer Society, 1998.

## 1.6 Terminology <a name="introduction-terminology"></a>
| Term | Description |
| --- | --- |
| User | Any living being who is interacting with the software is a _user_.|
| System | The package of all the components which takes input and gives output to demonstrate the features of the software is called System. |
| Database | Collection of information on different topics related to each other. |
| Library| The collection of tracks inside a directory or across multiple directories forms up a _library_.|
| Store | This is the persistence layer of whole system. |
| Metadata | The set of data which describes and gives information about the sound track. |
| Recommender system | A system which takes a track as input and outputs set of tracks closely related to the input. |
| Classifier| An algorithm that implements classification, especially in a concrete implementation. It is the part of _recommender system_. |
| Tags | A label attached to track which gives extra information about it. |
| NIC | A network interface card (NIC) is a computer circuit board or card that is installed in a computer so that it can be connected to a network |


# 2. Overall Description <a name="od"></a>

## 2.1 Product Perspective <a name="od-pp"></a>
This system consists of three components packaged as one desktop application:

- **Music player**: for playing music from local library.
- **Classifier**: On the bases of present track playing, Classifier will generate suggestions.
- **Metadata updater**: It update all the tracks in library with their metadata tags. This is done using already available online database like "[MusicBrainz][musicbrainz-website]".
- **Local Store**: It is implemented as a [SQLite](https://www.sqlite.org) database which acts as a map between track titles, paths and keeps a check on each track for its metadata information.

With _music player_ user can play/pause/stop/seek a track. It is a fully functional music player like any other music player currently available.

_Classifier_ needs some track title and metadata as input to generate suggestions. On the bases of
input track it suggests similar tracks which may be already available in local library or available on The Internet.

_Metadata updater_ is very similar to MusicBrainz's [Picard][picards-website] software. It takes a sound track or list of sound tracks as input and update their metadata information according to information available in [MusicBrainz database][musicbrainz-database-website]. This component needs internet for functioning.

_Local database_ maintains a list of tracks along their path in system which user wants to listen and mark them as updated and not updated on the bases of their synchronization with MusicBrainz database. This helps the system to keep all the tracks updated and minimizes the need of updating whole user library at once which may slow down the system.

#### Component Diagram
![](https://raw.githubusercontent.com/ProjectRecommend/docs/master/design-docs/final/images/Component_Dirgram_PR.jpg)


## 2.2 Product Functions <a name="od-pf"></a>
Using this app, user can play tracks available in offline library. While playing music user can get a list of suggested tracks which are most closely related with the present track in terms of their metadata tags like singer, genre, release year, rating etc. These tracks may be present in offline library or online sources.

User can perform following actions:

- play/pause/stop/seek, control volume
- add tracks/ remove tracks
- update metadata
- get recommendation

## 2.3 User Classes and Characteristics <a name="od-ucc"></a>
Almost any user will be able to easily get going with this application as it is perfectly meant for an average music lover. Music lovers especially interested in playing various genres of music in a playlist for background music playing for instance will be benefitted more than ever by this application as it does not require internet for playing the music.

Users with poor internet connectivity will benefit even more because the only place we require internet connection is where we are required to update the metadata of the music for giving correct suggestions.


## 2.4 Operating Environment <a name="od-os"></a>

#### System Requirements

- Operating System should be capable of playing music and have any of mentioned OS installed
- internet Connection is required for suggestions and metadata updation

#### Platforms Include

##### GNU/Linux

- CPU Type : Pentium 4 or higher; 2 GHz or higher
- Memory/RAM : 1 GB minimum, up to the system limit
- Hard Disk : 4 GB or higher
- Graphics : X Window server or similar graphics server

##### Windows

- Processor: 1 gigahertz (GHz) or faster.
- RAM: 1 gigabyte (GB) (32-bit) or 2 GB (64-bit)
- Free hard disk space: 16 GB.
- Graphics card: Microsoft DirectX 9 graphics device with WDDM driver.


## 2.5 Design and Implementation Constraints <a name="od-di"></a>

For recommendation of music we are using metadata available in individual tracks to implement [_**content based filtering**_][content_based_filtering_wikipedia].  

In [_content based filtering_][content_based_filtering_wikipedia], tracks are grouped into different views on bases of their metadata(properties like genre, singer, mood etc) which is already available. Unlike _collaborative filtering_, user behavior is not analyzed here and this may lead to less accurate results. Also this method needs a standard metadata schema over all the tracks that is the reason we are using [_MusicBrainz database_][musicbrainz-database-website] here.  


We could have implemented [_collaborative filtering_][collaborative_filtering_wikipedia] for generating suggestions which is more accurate then metadata approach but because we don't have user data and there is no user data available in public domain so due to lack of training data we cannot implement that.

The other way is [_waveform analysis_](http://www.academia.edu/4631247/Waveform-Based_Musical_Genre_Classification). In this method sound tracks are analyzed and grouped into different genres according to their waveform but it was found that this method is inaccurate. This technique is under research and development and is not proven successful.


## 2.6 User Documentation <a name="od-ud"></a>
- There is a user manual that lists all the features available for the user and methods to access them.
- "Help" option will be available in user interface which will redirect to Project Recommend [Website][project-recommend-website].

## 2.7 Assumptions and Dependencies <a name="od-ad"></a>

We used various online open source material for most of our project work. We integrated various components from other projects in order to make the application work as a whole.

The following lists the various open source material we had referred to:

- Music database [**_musicbrainz_**](https://musicbrainz.org/)
- music tagging application [**_MusicBrainz Picard_**](https://github.com/metabrainz/picard)
- Handling of audio metadata using [**_mutagen_**](https://github.com/nex3/mutagen)
- Music player [**_cherrymusic_**](https://github.com/devsnd/cherrymusic)
- Python cross platform GUI toolkit [**_PyQt_**](https://github.com/pyqt)
- [**_Sci-kit learn_**](http://scikit-learn.org) for Classifier


# 3. External Interface Requirements <a name="eir"></a>

## 3.1 User Interfaces <a name="eir-ui"></a>

User interface is implemented in PyQt that is a python library. There is one front page which interacts with user. It is divided into frames for different functions.

#### UI Mockup
![](https://raw.githubusercontent.com/ProjectRecommend/docs/master/design-docs/final/images/mockup.png)


## 3.2 Hardware Interfaces <a name="eir-hi"></a>
- Input device is needed for user to interact with system.
- Software needs a display device to interact with user.
- Music player needs playback device for sound output.
- Working Network Interface Card(NIC) for internet connectivity

## 3.3 Software Interfaces <a name="eir-si"></a>

TBD

## 3.4 Communications Interfaces <a name="eir-ci"></a>
- The Internet connection is used by [_Metadata updater_](#od-pp) and _Classifier_ to communicate with [_MusicBrainz Database_][musicbrainz-database-website].
- Internet communication will be Encrypted
- All Network Communications will use HTTPS/TLS

# 4. System Features <a name="sf"></a>

Following is the use case diagram for the application
![use case diagram](https://raw.githubusercontent.com/ProjectRecommend/docs/master/design-docs/final/images/PR_Use_case.jpg)

-----

##### Use case description table

| Use Case Title (ID) | Description | Remarks |
| --- | --- | --- |
| Manage Songs (UC1) | generalization of Manage songs |   |
| Control Music (UC2) | generalization of control songs |   |
| Manually Get Next recommendation (UC3) | user triggered recommendation |   |
| Edit Metadata (UC4) | user edits metadata |   |
| Manually update metadata (UC5) | user manually triggers metadata updation service |   |
| Control Volume (UC6) |  use controls volume |   |
| Play (UC7) | user can play music |   |
| Pause (UC8) | user can pause |   |
| Seek (UC9) | user can seek into timeline of playing track |   |
| Stop (UC10) | user can stop the playing track |   |
| Next Track (UC11) | user can change to next track |   |
| Previous Track (UC12) | user can go to previous track |   |
| Add songs (UC13) | user can add songs |   |
| Remove Songs (UC14) | user can remove songs from list |   |
| Access Local Storage (UC15) | components can access local storage for persistence  |   |
| Read from local Storage (UC16) | components can read from local storage |   |
| Write into local Storage (UC17) | components can write into local storage |   |
| Update into local Storage (UC18) | components can update data into local storage |   |
| Delete from local Storage (UC19) | components can delete items from local storage |   |
| Run Classifier (UC20) | components can run classifier on a track |   |
| Get data from MusicBrainz (UC21) | components can get metadata of a track from musicbrainz servers |  |
| Get Recommendation (UC22) | components can get recommendation on a track |   |
| Update Metadata (UC23) | components can update metadata of tracks |   |


----

#### Functional Requirements

| **Identifier for Requirement** | **Functional Requirement Name** | **Description** |
| --- | --- | --- |
| RQ 01 | Manually recommend music | The user will be able to get recommendations of any track manually, i.e., simply by right clicking |
| RQ 02 | Edit fields in the song info | The user will be able to edit info of any track manually, i.e., simply by right clicking |
| RQ 03 | Manually update metadata | The user will be able to update the metadata of any track manually, i.e., simply by right clicking |
| RQ 04 | Volume control | The user will be able to increase or decrease or mute the volume of the playing track |
| RQ 05 | Play music | The user will be able to play the track by selecting it or clicking on Play |
| RQ 06 | Pause music | The user will be able to pause the track being able to play it again from the same timeline |
| RQ 07 | Seek track | The user will be able to move anywhere in the timeline of the track |
| RQ 08 | Stop music | The user will be able to stop the track which will close the track, in order for the user to play another track or exit software |
| RQ 09 | Go to the next track | The user will be able to play the next track |
| RQ 10 | Go to the previous track | The user will be able to play the previous track |
| RQ 11 | Add songs | The user will be able to import music from his external music collection, to the application |
| RQ 12 | Remove songs | The user will be able to remove any track from the playlist |


----


**Project Recommend** comes with the following set of system features

#### Music player

Built into the offline music recommender system is a music player that can play music with a number of controls including **play, pause, stop, play next or previous track, seek and volume control**.

- The user will be able to import music from his offline music collection which may simply refer to a hard-drive or a flash memory.

- In import stage software will build an Internal Local Store with Information about added tracks.

- User can remove a track from imported music and that will remove the corresponding entry from Local Store

#### Local Store

- Local Store is persistence layer of application, it will be implemented as SQLite Database.
it will store all the information required for software to work

- The user will be able to essentially cache data into a local store while importing a track into the application.

- The Local Store will be storing the **the file path of the track, whether the track has been correctly tagged or not, the MusicBrainz track id and the id of the track.**

- On adding a track or importing a track from the offline music library of the user to the application the track will be added into the local store.

- On removing the track from the application the track will also be removed from the Local store. In short the Local store maintains the library of the application.
- It will not be available for user to direct interaction, This component will be used by other components internally.

#### Music Metadata Updater

- This component of the application is simply involved with updating the metadata or tags of music optionally from MusicBrainz database.

- This component is involved in 2 different situations:
    -  Firstly if the user plays a track and Classifier gets triggered and if metadata for that track is not updated This component will be triggered by classifier.
    - Secondly the user can Manually trigger metadata updation.

#### Classifier

- The classifier is the core of this application as it takes the heavy lifting of suggesting the right tracks for the user.

- The classifier comes into effect in 2 different situations

    - Firstly when the user chooses to play the music, the currently playing track will automatically be used for getting suggestions, play process will trigger the classifier.
    - Secondly the user can get suggestions on a track that he/she is not playing. In that case also the classifier will be used. in that case use will manually trigger Classifier on particular track.

#### Musicbrainz database

- The Musicbrainz database is the primary database for collection of **correct** music metadata and it contains almost every single track.
This database is used during metadata updation and getting data for classifier to generate suggestions.

#### User actions

This section will state all the use cases of the application and what the user will be able to do with the application.

**Music management**

The user will be able to manage music, import and export. The user will be able to import music files from offline music collection and also remove music files from the application.

**Control music**

The user can control music in the music player component by the following actions:

- play music
- pause music
- control volume
- go to the next track
- go to the previous track
- seek a playing track

**manual updation of metadata**

The user will be able to manage metadata of the tracks that he/she chooses.

**manual recommendation of music**

The user can get recommendation of a track manually by clicking on it.

A summary of the direct actions that the user can take is as follows:


#### User Interactions

The following are the use cases and how the actor: user interacts with them

**Use case: Manage tracks**

**Brief Description**

The user manages tracks, can import and remove them from the application

**User interaction**

- Import tracks from offline music collection
- Add directories, sub directories and files to the music player.
- The user can remove the track from the application
- The local store updates itself deleting the track

**Use case: Control Music**

**Brief Description**

The user can control music which means he/she can play, pause, stop, go to the next track, go to the previous track, control the volume

**User interaction**

- Click events trigger all controlling of music operations.
- On playing a track, the play process triggers an event that gets recommendations for the track
- The system checks whether the metadata is already updated or not, if not then the metadata is updated in the track
- The system connects to the Musicbrainz database to update the track metadata.
- The system fetches tags of the track.
- After metadata updation the local store is updated for the current track.
- The system then runs classifier on the track and gets all suggestions for that track.
- The suggestions are updated into the local store.

**Use case: Manually get recommendation**

**Brief Description**

The user can manually get recommendation of a track other than the track that is being played.

**User interaction**

- The user triggers event of getting recommendation of a track.
The system checks whether the metadata is already updated or not, if not then the metadata is updated in the track
- The system connects to the Musicbrainz database to update the track metadata.
- The system fetches tags of the track.
- After metadata updation the local store is updated for the current track.
- The system then runs classifier on the track and gets all suggestions for that track.
- The suggestions are updated into the local store.


**Use case: Edit metadata**

**Brief Description**

The user can also manually edit his/her track's metadata

**User interaction**
- The user defined metadata of a track is going to be updated in the local store.

**Use case: Manually update metadata**

**Brief Description**

The user can manually trigger updation of metadata of a track such that he/she can simply click on a track and update the metadata.

**User interaction**

- The user triggers an event of manually updating the  metadata of a track
- The system connects to the Musicbrainz database.
- The system fetches the metadata of a track from the database
- The system then updates the metadata into the local store.


# 5. Other Nonfunctional Requirements <a name="onr"></a>

The non-functional requirements of the system are explained below.

| **Non-Functional Requirements** | **Name** | **Description** |
| --- | --- | --- |
| **5.1  Performance Requirements**   |
| NR_01 | Quickness | System should be fast enough to play music and respond to any of the user action in any way without any shattering or buffering, else it will be not be a good experience. |
| NR_02 | Robustness | System should be robust to deal and act accordingly with common error scenarios like no internet connection, unavailable metadata, unsupported file types. |
| NR_03 | Failure Handling | In case of failures it should be able to fail or recover quickly. |
| **5.2  Safety Requirements**   |
| NR_04 | Exception Handling | The software should be able to restrict or warn(in the first place) the user from doing things not suitable, like, increasing volume beyond threshold, or exiting the software w/o saving the changed data. |
| **5.3  Security Requirements**   |
| NR_05 | Encrypted Connection | Connection between user and [MusicBrainz](https://musicbrainz.org/) servers should be Encrypted (HTTPS/TLS). |
| **5.4 Software Quality Attributes** |
| NR_06 | Memory Management | System should not leak memory. |
| NR_07 | Compatibility  | System should peacefully co-exist with other software |
| NR_08 | Error Handling  | System should not cause or trigger any events that will leave Operating System in unrecoverable state |
| **5.5 Business Rules** |
| NR_09 | Open Source | This software is an Open Source software. |
| NR_10 | Guidelines | Unless required by applicable law or agreed to in writing, software distributed is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. |



# 6. Other Requirements <a name="otherreq"></a>

TBD

# Appendix <a name="appendix"></a>

- Source for outline of this SRS Document : [Wikipedia](https://en.wikipedia.org/wiki/Software_requirements_specification#Structure)

------------------

[musicbrainz-website]: https://musicbrainz.org
[musicbrainz-database-website]: https://musicbrainz.org/doc/MusicBrainz_Database
[picards-website]: https://picard.musicbrainz.org
[collaborative_filtering_wikipedia]: https://en.wikipedia.org/wiki/Collaborative_filtering
[content_based_filtering_wikipedia]:https://en.wikipedia.org/wiki/Recommender_system#Content-based_filtering
[project-recommend-website]: https://projectrecommend.github.io/
