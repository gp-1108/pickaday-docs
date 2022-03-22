---
title: Pick a Day Backend

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - event
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the pickaday API
---

# Introduction

Pick a day is a simple app event based. The main goal of the API is to store plausible dates for an event, allowing partecipants to choose whether they are available or not in a day of the main event. It is therefore possiple to see who can join when in a selected event.

There are two main type of objects in pickaday:
* Events
* Partecipants

An **Event** is defined by:

* a unique ID
* the days in which it could take place
* the name of the event

A **Partecipant** is defined by:

* Its name
* the event it partecipate to

<aside class="notice">
Multiple events with the same name and dates can be created without problems.
</aside>

# Authentication

This API does not require any previous authorization. Its endpoint can be accessed freely.
