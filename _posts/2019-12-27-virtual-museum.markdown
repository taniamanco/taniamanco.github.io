---
layout: post
title:  "Virtual Museum js"
date:   2019-12-27 08:00:00 -0400
categories: from zero to tech
---

The Virtual Museum application allows users to express their taste in art through virtually curated exhibits.  The App integrates various art/photography sources such as Unsplash (https://unsplash.com) and serves as an excellent way to show the fantastic work of artists and photographers around the world. 

The project incorporates different technologies in its stack — RoR (Ruby on Rails) as its backend and a SPA (Single Page Application) on its frontend. 

**The backend**

A straight forward RoR application with few data models and a RESTful API.

**Models**

Exhibit: Represent an exhibit and serves as a container for the exhibit items selected by the user.

ExhibitItem: Captures the details of a singular art/photographer piece, such as artist name and a URL of the item.

Integration with Art/Photography providers
The backend serves as a proxy between the client and the integrated provider. This proxy allows to prevent exposure of credentials to the client when interacting with their APIs. Credentials defined as environment properties that can be configured via the standard Rails configuration mechanism.

**The frontend**

A Single Page Application backed by a single HTML document split into functional sections (screens) with a router on top, helping to navigate between them. Each section supported by a dedicated controller which drives logic and communication with the backend server.

**Router**

The Router is the backbone of the App. By listening to hash change event and mapping routes to controllers, it orchestrates the transition between sections (screens/pages) and binds views to controllers.

**Controller**

NavigationController - Orchestrates and manages the navigation bar.
ExhibitListController - Serves as the main entry point to the application.  Surfaces up existing Exhibits and allows users to explore and view the various Exhibits curated by other users.
ExhibitCurationController - It all starts with curation. This controller is responsible for building up the Exhibit. It integrates with Unsplash through the proxy and allows searching and matching items for the Exhibit.
ExhibitViewController - This controller is where magic happens. Users can experience the Exhibit and view its items as other users curated them.

**Putting things together**

For convenience, I made a seed file for three exhibits to test. 
Run the following commands: 
```
bundle install
```

Followed by :
```
bundle exec rails db: migrate
```
and 
```
bundle exec rails db: seed
```
when all seeded and set run 
```
bundle exec rails s
```
Now, as the App running, you would be able to navigate to any of the exhibits and see individual items and delete exhibition. As well, you can curate your Exhibit by navigating to the 'Curate' section and search your interests and hobbies. The App is flexible and gives the option of having a few searches without losing chosen optional images. 
