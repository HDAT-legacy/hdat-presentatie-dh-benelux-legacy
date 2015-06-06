# The Brown Map

# Historical Dutch Asiatic Trade

## Introduction

Good Afternoon all! We’re here to show you a visualization project of the VOC, the “Vereenigde OostIndische Companie”, or the Dutch East Asiatic Trading Company which operated the 17th and 18th century. To introduce ourselves quickly: that’s Erik and I’m Robert-Jan. We’re both students at the University of Amsterdam. Art History for me and History for Erik. We both have an interest for the Digital Humanities which was jumpstarted by a course called ‘Coding the Humanities’, where we spend month coding and talking about it’s relation to the Humanities. This led us to think about the Humanities in another perspective than our studies provide, and pursue coding further. Anyways, a few months later Erik dug up a database about VOC for another DH-course, I jumped in, and slowly this project took shape.

## Contents

Today I’m going to be talking mainly about the realization of preliminary product we’ve made and the academic and technical concerns that come with it. I’m not going to be interpreting it today, we simply cannot yet asses its value because we’ve not properly connected it to the academic discours yet. Contrary to most research, we do don’t go in with a specific question. Instead We’ve taken a data-centered approach when making this. This brings me to the first part of the presentation where I’ll introduce you to the data available. Secondly I’ll discuss how the tool came to be. Then I’ll discuss the tool itself, it’s academical aspect and it’s technical aspect. To close the presentation off, I’ll show you a few feature’s which weren’t finished to show here today, and speculate a bit about where we plan to take this.

## The Data 

You all probably know the VOC or the Dutch East India Company or at least the concept of an East India Company. But just to be sure: the VOC was a trading company established in 1602 for the trade on the East Indies. Its basically about ships, trade, exotic lands, but also a lot corruption and exploitation. It was by far the largest trading company of the time and it was considered the first multinational. However you can read all about this on wikipedia or if you’re more decent: there are plenty of books. What’s interesting to us however is that it’s sheer size forced it to have a decent bookkeeping, and a lot of that bookkeeping is preserved. Even more importantly: much of it is digitized. This is the basis for our project.

Like I said before, from the start we took a very data-oriented approach. The actual database we discovered was the Dutch Asiatic Shipping, an database containing voyages from Amsterdam to East India. Yet soon we noticed there was an even better database, just digitized by the Huygens/ING, the BGB. This database was created from the extensive bookkeeping of the the ‘Boekhouder Generaal Batavia’. These books currently lie in the National Archive in The Hague. This source contained an amazing amount of data. 18.000 voyages of ships going from The Netherlands to East India and also quite a bit of trade within Asia. The records contain dates, names and value. It also logged the goods aboard those ships, which add up to 250.000 records! In those records are their value and many other measurements. Yet the BGB was presented online as just another database, quite meaningless if you don’t have a specific question. So we thought what if we visualized it geographically? 

Next to the DAS and BGB databases there are a few more interesting databases around. First off: the Atlas of Mutual Heritage. These guys geographically encoded many locations and added information to it. That saved us a lot of work in actually having to look everything up ourselves. Secondly there is the Climatological Database for the Worlds Oceans. This database shows routes ships used to take from historical logs. We’ve used this to construct the route networks the ships use. In addition to that we’ve used some traditional research and looked at maps from the “nieuwe groote ligtende zee-fakkel”. Thirdly there is VOC-opvarenden database, which contains an amazing amount of people whom travelled with VOC vessels: 655.000. These guys travelled for good or for bad. A quick count showed 80.000 people died aboard ships. But while extremely interesting, we’ve not used this database, yet. 

## Realisation

We started ideating about the stuff we could do, which was quite like Europa Universalis. A cool but way to complex game, just a bit more academically sound. But soon we we’re confronted with reality. Cool, all this data. But how do we actually open the database and perform mutations onto it? What is an geographical information system and how do they work? How do we implement it on the web? Mind you, we only had 12 ECTS of actual training, so we had to learn quite a bit on our own. We spend a month looking over the web, finding tools, experimenting with them a bit, trying to create the basic building blocks of what we needed.

And at the same time we we’re always having the discussion as to its relevance. What does the visualization actually have to do and show? The VOC is a big theme in history, and much researched field, can we add to it? There is an overload on resources. It’s actually so central that it lives in collective memory with our prime-minister Balkende quoting the “VOC mentaliteit” and movies like the recent Michiel de Ruyter. Yet these things also show a lack of knowledge of what it was actually like. In both perspectives on corruption and exploitation are absent. But also perspectives on size, location and the actual driving forces are often missing. The numbers are often quite questionable, knowing the available data. We had two main goals. Firstly we wanted to provide a narrative that was both beautiful and easily accessible. Secondly, and much more ambitious, we wanted to create a tool that provides an easy interface to the data for academia.

## The Tool

Enough talk, the actual tool now. We’ve got video’s in our presentation because of presentation purposes. But the actual tool is available on thebrownmap.nl. Mind you, it’s still a prototype and doesn’t contain the entire dataset due to reasons I’ll go into later.

What you’re seeing is actually three layers: the first and most prominent is the historically styled satellite map. Secondly there is a route network, which might not be visible that well here. On the third layer are the actual ships, visualized by dots. At the moment the interface allows you to interact with the map, manipulate time, and click the voyages. These currently link back to the Huygens/ING. We will expand on these features in due time. Right now we were actually quite happy we had the main visualization ready to show in time for this conference. 

I think it’s interesting the go into how it actually works in a bit more detail. The database provides us with a voyage record. This record contains information about the departure times and the locations. Our code properly transform these records so that the machine can understand them, the time gets formatted correctly and the written locations are transformed to coordinates. These coordinates then get applied to the routing network, which returns us the shortest route. Taking into the wind into account to a certain measure. When it’s done calculating all of this information is bundled up into our web-app. The web application takes the time and animates an icon over the given route.

As it is, we think it already provides some curious perspectives. I won’t go into interpreting it exactly yet, mainly because we’re still lacking proper contextual research. 

## Academical Concerns

We can tell you what we did however, especially about the problems and decisions we encountered. There is a lot going on under the hood, academically speaking. We’ve decided right from the start that everything we did had to be clearly logged. This is why we chose to never interact with the dataset barehanded, editing field to our requirements. All our steps a logged into the actual code, and are repeated every time when we compile the app. If someone wants to know or check what we’ve done: our scripts are our logs. Secondly the entire project is version controlled, every step we’ve made is saved. You can see it’s history from no code to the project that is visible now, for each file individually if you so desire.

Just logging everything isn’t enough though. There are some important choices we had to make. The nature of the data is that bookkeeper who wrote everything down, ’the Boekhouder Generaal Batavia’, was situated in Batavia. So he only knew either the arrival data ór the departure date. We had to extrapolate the other. Right now we do this on basis of a simple speed: 5km/h. There is little magic now. But it’s simulated history non the less. We’ve got plans to improve this however, when we add the database from the Dutch Asiatic Trading back into the mix. This database has departure ánd arrival dates for many ships, which will lessen the amount of simulation. While actually having an interesting field more, we chose not to start with this one because it mainly contains ships traveling from the Netherlands to East India. The BGB also has trade within Asia, and much more detail on what the ships carried.

The third concern we had was to know how the ships travelled to Asia. Unfortunately the ships didn’t use GPS coordinates and noted them down every minute or day. To counter this lack, Erik went to the archives and looked at quite a bit maps and tried to construct the route network over which we route the ships as I previously explained. He also used the Climatological Database for the Worlds Oceans quite a bit, which shows the routing of ships from 1750-1850, towards the end of the VOC. From these sources he constructed a route network, by eye, over which the ships are routed. Important to know is that this network is coded as a module, it could be swapped out by another in a minute or so.

In both of these cases we go from a general notion of how thing went, and project that on individual cases. This is speculation but unavoidable. We will simply never know exactly what route a ship has taken, or where it was at, at a certain moment in time. Spatial and temporal distortions are inescapable when visualizing history like this. Although we dare say it already gives a better idea of where a ship might have been, than any rough estimation by a researcher. We’ve connected as many sources of information as we could find and tied them to each other. Much of history will always be guessing, geospatial history is no different in that regard. You can only make your assumptions as clear as possible. 

One project that quite like ours deals with the same problem. Orbis: The Stanford Model of the Roman World. We’re actually using the more or less the same tech stack. These guys have spend quite a bit of time detailing each of these decisions out.  We account for wind with like say, this route is bad for return journeys. They have actual wind simulations running. We simply do not have the resources to detail it out that much, you’re seeing our Fridays and weekends. On the other side we have it easy in comparison to them, we have full and rich datasets. Which are quite certain in comparison to theirs, but are they certain enough? Are they certain enough to insinuate the actual position in space and time of real historical entities? Then there is also another key question of a more general nature: to what extent does the database cover what actually happened? We don’t even have a rough estimation of how much of the actual voyages are represented in the database.

Our rich sources also provide us with another problem. Right now we’ve got another discussion amongst ourselves where we have to chose between a correct narrative or trying to stay close to our source. If you view the visualization right now, you’ll note that there are many ships visualized almost at the same location with the same name. This is because of the source, voyages are separated into multiple records, which overlap. Do we want to make the narrative ‘correct’ and transform the notion of a voyage into that of a ship, or do we want to stay close to the source? We might also decide to branch out here and make two versions, however we then have to deal with the added maintenance. Our two goals are in conflict here: will the narrative aspect or the academical tooling side claim supremacy? 

## Technical Concerns

As to so far the main academical concerns. The technical stuff is also there. We had several things to consider for this one. First of, we we’re taught web-based tools. This is a great thing, but also a limitation. We don’t have much resources at our disposal for rendering stuff. This is the reason that we don’t show the full dataset right now, it would slow many computers down to a halt. We’ve swapped out technologies for this several times. But there are also advantages. We’re working straight in an environment that is always published right away. This means user interface is immediately a concern. The obvious advantage is that you can immediately see, try, and test it. 

All of the things in this list are individually actually quite simple and you can learn them quickly. To learn all of them however takes time. Even we both still have our specialities on the project: I barely know anything about the tile-generation. Erik knows less about the temporal logic. But we both know the important hinges in the program. 

### Build:
- Git and Github for version control - the code is opensource and downloadable there.
- Gulp and Shell scripts for the build-process
- PostgreSQL, PostGIS and PG-Routing for the geographical stuff.
- QGIS to create the route network 
- Tilemill to create the map

### Client-side:
- Default webstack: HTML / CSS / JS
- Leaflet (for the map) with a plugin Leaflet Playback (heavily edited)










### Build side (optional)

First off the building side of things. The version control I spoke about before, well that is done with Git and Github. This is a tool by which you have explicitly define what changes you want to ‘commit’ the ‘repository’. It’s quite cool, especially if you’ve used it a while and know the command line interface that comes with it. I’ve actually started using it for writing papers and stuff. 

Secondly build-automation, we hate telling the database everything to take in a clean version of the BGB data, mutate it, take in the route network etc. etc. So we use tools for this, right now those are a few shell scripts and the task runner Gulp. I’ll won’t go into these as they are quite specific, just remember the concept that the more you can automate the better it is.

Thirdly the choice of Database Management System. The Huygens institute send us a MySQL database, yet MySQL didn’t offer us enough out of the box functions. We had to convert to PostgreSQL because of it’s extensibility with PostGIS and PGrouting. These two are quite cool, PostGIS has all kinds of functions out of the box for geometry. We didn’t have to call upon that geometry learned in high school, the math/ICT guys did that for us. PGrouting is again an extension of PostGIS. This tool is basically a routing feature like in Google Maps. You give it two coordinates and a route network, and it give you back the shortest route. I’d say this stack is the most involved to learn, you have to learn SQL and to use functions pl/pgSQL. A nice additional tool in this context PSequel, which provides a graphical interface to the database to view what you’re doing. 

That brings me to the last tool QGIS. QGIS is a graphical interface to manipulate geographical data. It can process all geographic information and give you insight in what you have before you actually have your app done. It also can be used to create geographical data like we did for the routing network. It’s quite good, and easy to use if you’ve got no understanding at all. I can be a little counter-intuitive at times though, but you get over it quite quickly.

As a side note: the map you’re seeing was created with Tile-mill. The program allows you to edit maps to your liking, and then export the tiles you desire.

### Client side (optional)

First and foremost the basic and age-old web-stack: HTML, CSS, Javascript. To do anything custom on the web you simply need to know these. You will be able to do something cool with it quite fast, but it’s a large stack. To know it well will take some time. But the rewards are great, you’ll probably use them quite a bit. Every project now-a-days needs a website, and people whom can edit them. Even the e-pub standard uses CSS. These languages are everywhere. 

Aside from the basic web-stack we actually barely did anything. We included the library Leaflet, which does all the mapping stuff for us and provides a very clean API. Again the ICT guys did all of the hard labour and provided us with simple tools. Form the temporal element in the visualization we used the plugin Leaflet Playback. This plugin we needed to edit here and there, because our demands we’re quite a bit more heavy than it was build for. But most of the logic is precisely the same.









## Future

Right now you’re only viewing a prototype. We’ve kept the interpretation deliberately open in our presentation because we simply do not know yet what all of this tells us. We haven’t really had the time to do good contextual research. Erik is going to try to write his thesis on the subject so it should have a document in coming year that explores the tool and the information it provides from a proper academic viewpoint.

Besides that we plan to add additional features. Academically interesting is a feature we’re already well on our way of implementing. We’ve enumerated on the goods in the database and build a layer that can visualize basic Minard diagrams. It not even close to finished, but it already showing cool things. Things like evangelical goods to show the attempts at spreading religion, or the amount of military goods to show military capability. Those could prove to be quite interesting if one is able to generate graphs and review them with a simple click. The latter will require one to be able to view the goods inside the visualization. Right now you get thrown to the BGB site if you click a ship.

We’ve also got plans to add a few other layers for narrative, like major events to contextualize what is shown for people who’ve got no idea of them. There are many interesting events like wars, the closing and opening of diplomatic relations, etcetera. Together we hope to provide an interesting environment to explore the VOC in a decent manner. Besides that we’ve still got plenty of ideas to burn trough, but eventually time will determine how far we’ll get with that. Im out of time I believe.  We’d really appreciate to know what you think! Test the app and leave a comment. We’re also the demo later on, but you can find it online here:

www.thebrownmap.nl

Also to close off, we would really like to thank all our teachers at the University of Amsterdam and the Vrije Universiteit. In particular Marijn Koolen and Jan Hein Hoogstad and their project Coding the Humanities / Unacademic for teaching us and sponsoring us to actually be here! 

## Questions!
