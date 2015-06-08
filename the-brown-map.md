# The Brown Map

# Historical Dutch Asiatic Trade

## Introduction

Good Afternoon all! Erik and I are here to show you a visualization project of the “Verenigde Oostindische Compagnie”, or the Dutch East Asiatic Trading Company, called “The Brown Map”. To introduce ourselves quickly: that’s Erik and I’m Robert-Jan. I study Art History at the University of Amsterdam and Erik studies History there. We both have an interest for the Digital Humanities which was jumpstarted by a course called ‘Coding the Humanities’. In this course we spend month coding and talking about it’s relation to the Humanities. This has led us to think about the Humanities in another perspective than our studies provide, and pursue coding further. This project itself took shape when Erik dug up a database about the VOC for another DH-course and I jumped in to help him. 

## Contents

Today I’m mainly going to be talking about the realization of preliminary product we have made and the academic and technical concerns that come with it. I’m not going to be interpreting it, because we simply cannot asses its value yet. We still have to properly connect it to the academic discours. Contrary to what we we’re thought in our normal studies, we didn’t go in with a specific question. Instead we’ve taken a data-centered approach when making this. The data is also going to be the subject of the first part of this presentation, where I will give an introduction to the available datasets. Secondly I’ll discuss how the tool came to be. Then I’ll discuss the tool itself, it’s academical aspect and it’s technical aspect. To close the presentation off, I’ll show you a few feature’s which weren’t finished in time to show here today, and speculate a bit about where we plan to take this.

## The Data 

All of you probably know the VOC or the Dutch East India Company or at least the concept of an East India Company. Just to be sure however, the VOC was a trading company established in 1602 for the trade on the East Indies and existed until the end of the 18th century. Its basically about ships, trade and exotic lands, but also about corruption and exploitation. It was by far the largest trading company of the time and it was considered the first multinational. However you can read all about this on wikipedia or if you’re more decent: there are plenty of books. What’s interesting to us is that it’s sheer size forced it to have a decent bookkeeping, and much of that bookkeeping has been preserved. Even more importantly: much of it is digitized. This is the basis for our project.

The first database we discovered was the Dutch Asiatic Shipping, an database containing 3500 voyages from Amsterdam to East India. Yet soon we noticed there was a more detailed database, just digitized by the Huygens/ING, the BGB. This database was created from the extensive bookkeeping of the the ‘Boekhouder Generaal Batavia’, from which it gets its name. Currently it lies in the National Archive in The Hague. This source contained an amazing amount of data but it was written in Batavia. It contains 18.000 voyages of ships going from The Netherlands to East India and there also is quite a bit of trade within Asia. The records contain dates, locations, ship names and cargo. This cargo was not only logged by its value, but every item is described in detail. The total amount of goods logged add up to 250.000 records! 

Next to the DAS and BGB databases there are a few more interesting databases around. First off: the Atlas of Mutual Heritage. These guys geographically encoded many locations and added information to it. That saved us a lot of work in actually having to look up everything ourselves. Secondly there is the Climatological Database for the Worlds Oceans. This database shows the routes ships used to take from historical logs. Thirdly there is VOC-Opvarenden or VOC-Embarked database, which contains an amazing amount of people whom travelled with VOC vessels: 655.000 people. These guys travelled for good or for bad. A quick count showed 80.000 people died aboard ships. This is a quick summation of the important data available.

## Realisation

With all the data collected we started ideating about the stuff we could do, which looked in my mind quite like a computer game called Europa Universalis. Just a tad more academically sound. We had many features in our minds, and many more formed while we where working on it. But we where confronted with reality quite soon. It’s quite a bit of work. 

At the same time we we’re always having the discussion as to its relevance. We had to set some goals. What does the visualization actually have to do and to show? The VOC is a big theme in history, and much researched field, can we add to it? There is an overload on resources. It’s actually so central that it lives in collective memory with our prime-minister Balkende quoting the “VOC mentality” and movies like the recent Michiel de Ruyter. Yet these things also show a lack of knowledge of what things were actually like. In both perspectives on corruption and exploitation are absent. But also perspectives on size, location and the actual driving forces are often missing. The numbers are even more questionable, knowing the available data. We had two main goals. Firstly we wanted to provide a narrative that was both beautiful and easily accessible to provide the perspectives that the data offer. Secondly, and much more ambitious, we wanted to create a tool that provides an easy interface to the data for academia.

## The Tool

Knowing what we wanted we did some ugly experiments but we eventually ended up at the actual tool you’ve been seeing in the background all along. We have got video’s in our presentation because of that’s less likely to fail and doesn’t require interaction. But the actual tool is available on thebrownmap.nl. Mind you, it’s still a prototype, it could have bugs.

What you’re seeing is actually three layers: the first and the most prominent is the historically styled satellite map. On top of that there is a route network, which might not be visible that well here. Finally the white dots you’re seeing are the actual ships. At the moment the interface allows you to interact with the map, manipulate time, and click the voyages. These currently link back to the Huygens/ING. We will expand on these features in due time. Right now we were actually quite happy we had the main visualization ready to show in time for this conference. 

Okay, lets go into how it actually works in a bit more detail. The dataset provides us with a voyage record. This record contains information about the departure times and the locations. Our code takes this record and transforms it so that the machine can properly understand it, the time gets formatted correctly and the written locations are transformed to coordinates. These coordinates are then converted to nodes on the routing network. The Dijkstra Algorithm then takes the two nodes and the line-network, and returns us the shortest route. This route is then stored back onto the record. When it’s done calculating this for each record, the information is bundled up into our web-app, where it lies dormant until a user requests it. When the web-application is loaded, it takes the time and the determined route and animates an icon over it. The result you just saw.

## Academical Concerns

But what does it mean? The interpreting I’ll have to leave out for now, we are simply lacking proper contextual research. However as it is we do think it already provides a curious perspective on the data.

### Logging

We can tell you what we did however, especially about the problems we have encountered and decisions we have made. There is a lot going on under the hood, academically speaking. To counter this we have decided right from the start that everything we did had to be clearly logged. This is why we chose to never interact with the dataset barehanded. All our steps a logged into the actual code, and are repeated every time when we compile the app. If someone wants to know or check what we’ve done: our scripts are our logs. Secondly the entire project is version controlled, every step we’ve made is saved. You could see it’s history from no code to the project that is visible now, for each file individually if you so desire.

### Missing Data

Just logging everything isn’t enough though. There are some important choices we had to make concerning missing data. The nature of the data is that bookkeeper who wrote everything down, ’the Boekhouder Generaal Batavia’, was situated in Batavia. So he only knew either the arrival data ór the departure date. We had to extrapolate the other. Right now we do this on basis of a simple speed: 5km/h. There is little magic there. But it’s very much simulated history. We’ve got plans to improve this however, when we add the database from the Dutch Asiatic Trading back into the mix. This database has departure ánd arrival dates for many ships, which will lessen the amount of simulation. You’d wonder, why not start with that one, it has more of the information you need. We chose not to however. Mainly because this database only contains ships traveling from the Netherlands to East India. The Boekhouder Generaal Batavia also had trade within Asia, and much more detail on what the ships carried. Because of this we suspected that the BGB would yield a more interesting visualization. Beyond that, the database had much more structure.

Another missing piece of information was that we didn’t know how the ships travelled to Asia. Unfortunately they didn’t use the Global Positioning System back in the day, and noted the coordinates down every minute or day. To counter this lack, Erik went to the archives and looked at quite a bit of maps from the “nieuwe groote ligtende zee-fakkel” and tried to construct the route network over which we route the ships as I previously explained. He also used the Climatological Database for the Worlds Oceans quite a bit, which shows the routing of ships from 1750-1850, towards the end of the VOC. From these sources he constructed a route network, by eye, over which the ships are routed. However there is probably still some room for improvement here. It’s important to know that every part of this visualization is modularized, and could be swapped out by another in a minute or so.

In both the time extrapolation as in the determining the routes, we go from a general notion of how thing went and project that on individual cases. This is speculation but unavoidable. We will simply never know exactly what route a ship has taken, or where it was at, at a certain moment in time. Spatial and temporal distortions are inescapable when visualizing history like this. Although we dare say it already gives a better idea of where a ship might have been than any rough estimation by a researcher. We’ve connected as many sources of information as we could find and tied them to each other. Much of history will always be guessing, geospatial history is no different in that regard. You can only make your assumptions as clear as possible. 

### Comparison: Orbis

Another project that is quite like ours deals with the same problem. This is Orbis: The Stanford Model of the Roman World. We actually have more in common than appears on the surface: we’re using more or less the same tech stack. These guys have however spend quite a bit of time detailing each of these academic concerns out. We account for wind with like say, this route is bad for return journeys. They have actual wind simulations running. We simply do not have the resources to detail it out that much, after all you’re seeing our Fridays and weekends. On the other side we have it easy in comparison to them, we have full and rich datasets. Which are quite certain in comparison to theirs, but are they certain enough? Are they certain enough to insinuate the actual position in space and time of real historical entities? In Orbis you’re after all routing a fictional entity. 

Then there is also another key question of a more general nature: to what extent does the database cover what actually happened? We don’t even have a rough estimation of how much of the actual voyages are represented in the database. It is not the full VOC-activity that is visible. 

## Story or Academical Tool?

Another problem we encountered had to do with our goals. Right now we have got another discussion going amongst ourselves where we have to chose between a correct narrative or trying to stay close to our source. If you view the visualization right now, you’ll note that there are many ships visualized almost at the same location with the same name. This is because of the source, voyages are separated into multiple records, which overlap. Do we want to make the narrative ‘correct’ and transform the notion of a voyage into that of a ship, or do we want to stay close to the source? Another solution might be to branch out here and make two versions, however we then have to deal with the added maintenance. Our two goals are in conflict here: will the narrative aspect or the academical tooling side claim supremacy? 

## Technical Concerns

As to so far the main academical concerns. The technical stuff is also there. We had several things to consider for this one. First of, we where taught web-based tools. This is a great thing, but also a limitation. We don’t have much resources at our disposal for rendering stuff. This is why we don’t show the full dataset online right now, it would slow many computers down to a halt. It’s also why we do a lot of calculation while building the app. But there are also advantages. We’re working straight in an environment that is always published right away. This means user interface is immediately a concern. The obvious advantage is that it is published immediately. Everyone can see, try, and test it. 

Below is a list of the technologies we’ve used listed. All of the things in here are individually actually quite simple to learn. To learn all of them however takes time. Even we both still have our specialities on the project: I barely know anything about the tile-generation. Erik knows less about the temporal logic. But we both know the important hinges in the program. 

### Build:
- Git and Github for version control - the code is opensource and downloadable there.
- Gulp and Shell scripts for the build-process
- PostgreSQL, PostGIS and PG-Routing for the geographical stuff.
- QGIS to create the route network 
- Tilemill to create the map

### Client-side:
- Default webstack: HTML / CSS / JS
- Leaflet (for the map) with a plugin Leaflet Playback (heavily edited)

## Future

What does the future hold? First off, you can expect a document interpreting this visualization. Erik is going to write his thesis on the subject so it should have a decent document coming next year that explores the tool and the information it provides from a proper academic viewpoint.

Secondly that we plan to add additional features. This is only a prototype. Academically interesting is a feature we are already well on our way of implementing. We’ve enumerated on the goods in the database and build a layer that can visualize basic Minard diagrams. It still needs quite a bit of love, but it’s already showing cool things. Things like evangelical goods to show the attempts at spreading religion, or the amount of military goods to show military capability. The trade of metals also shows interesting patterns. All of these could prove to be quite interesting and academically trustworthy if one is able to generate graphs and review (and perhaps download) the data that constructed them with a simple click. We plan to add that. 

We’ve also got plans to add a few other layers for narrative, like major events to contextualize what is shown for people who’ve got no idea of them. There are many interesting events like wars, the closing and opening of diplomatic relations, etcetera. Together we hope to provide an interesting environment in which you can explore the VOC in a decent manner. Besides that we’ve still got plenty of ideas to burn trough, but eventually time will determine how far we will get with that. 

Im out of time I believe. We’d really appreciate to know what you think! Test the app and leave a comment. We’re also at the demo later on, but you can find it online here:

www.thebrownmap.nl

Also to close off, we would really like to thank all our teachers at the University of Amsterdam and the Vrije Universiteit. In particular Marijn Koolen and Jan Hein Hoogstad and their project Coding the Humanities / Unacademic for teaching us and sponsoring us to actually be here! That’s all, Questions?

## Questions!














### Build side (optional)

First off the building side of things. The version control I spoke about before, well that is done with Git and Github. This is a tool by which you have explicitly define what changes you want to ‘commit’ the ‘repository’. It’s quite cool, especially if you’ve used it a while and know the command line interface that comes with it. I’ve actually started using it for writing papers and stuff. 

Secondly build-automation, we hate telling the database everything to take in a clean version of the BGB data, mutate it, take in the route network etc. etc. So we use tools for this, right now those are a few shell scripts and the task runner Gulp. I’ll won’t go into these as they are quite specific, just remember the concept that the more you can automate the better it is.

Thirdly the choice of Database Management System. The Huygens institute send us a MySQL database, yet MySQL didn’t offer us enough out of the box functions. We had to convert to PostgreSQL because of it’s extensibility with PostGIS and PGrouting. These two are quite cool, PostGIS has all kinds of functions out of the box for geometry. We didn’t have to call upon that geometry learned in high school, the math/ICT guys did that for us. PGrouting is again an extension of PostGIS. This tool is basically a routing feature like in Google Maps. You give it two coordinates and a route network, and it give you back the shortest route. I’d say this stack is the most involved to learn, you have to learn SQL and to use functions pl/pgSQL. A nice additional tool in this context PSequel, which provides a graphical interface to the database to view what you’re doing. 

That brings me to the last tool QGIS. QGIS is a graphical interface to manipulate geographical data. It can process all geographic information and give you insight in what you have before you actually have your app done. It also can be used to create geographical data like we did for the routing network. It’s quite good, and easy to use if you’ve got no understanding at all. I can be a little counter-intuitive at times though, but you get over it quite quickly.

As a side note: the map you’re seeing was created with Tile-mill. The program allows you to edit maps to your liking, and then export the tiles you desire.

### Client side (optional)

First and foremost the basic and age-old web-stack: HTML, CSS, Javascript. To do anything custom on the web you simply need to know these. You will be able to do something cool with it quite fast, but it’s a large stack. To know it well will take some time. But the rewards are great, you’ll probably use them quite a bit. Every project now-a-days needs a website, and people whom can edit them. Even the e-pub standard uses CSS. These languages are everywhere. 

Aside from the basic web-stack we actually barely did anything. We included the library Leaflet, which does all the mapping stuff for us and provides a very clean API. Again the ICT guys did all of the hard labour and provided us with simple tools. Form the temporal element in the visualization we used the plugin Leaflet Playback. This plugin we needed to edit here and there, because our demands we’re quite a bit more heavy than it was build for. But most of the logic is precisely the same.










