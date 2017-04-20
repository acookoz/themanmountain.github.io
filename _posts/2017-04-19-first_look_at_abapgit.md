---
layout: post
title: First look at ABAPGit & ideas on a feature
---

I had my first opportunity to take a look at ABAPGit today and although it was not a win for the particular task I had to do, it made me
excited to think about the future of ABAP development.

A client has several web apps written in [AngularJS][angular], embedded in a BSP and hosted on a Netweaver Gateway ABAP Stack.  
The front end UI is served to the public via [Microsoft Threat Management Gateway][tmg] which is acted as a reverse proxy. The apps communicate via Gateway OData services to ERP.

The cost of the hosted TMG solution was fairly significant, and given that we have already produced and published some apps using
[SAP Cloud Platform][scp], the goal was to migrate these applications to SCP; a significant cost saving and a decent performance improvement.

I had thought that installing ABAPGit might be the easiest way to extract the html/css/js assets after discovering that the UI5 upload/download tool (/UI5/UI5_REPOSITORY_LOAD) didn't work with regular BSPs. In hindsight that was a bad idea (see later) but it
gave me an opportunity to get permission to install [ABAPGit][abapgit] and get a first glimpse of it.

The ABAPGit program itself is an HTML Viewer control embedded in the SAP GUI, which is a really welcome surprise when you mostly work with ALVs and Enjoy transactions all day. It's a fairly under-utilised method of building a traditional SAP GUI application - a main requirement for a project like this is to have a program that is self contained within a single ABAP object, and this is a clever way to complete that while still having a modern user interface.

Creating a new repository is as easy as giving it a name and specifying the associated ABAP package. From there you can either download to a zip to reimport into github, or make it an "online" project and push directly.


The Problem
===========

I created the project and specified the package which produced the object list below.

![ABAP Git object list][objectlist]

Of course the html/css/js files just show up as MIME objects title with a GUID (based on its object directory entry) - I should have realised that before I even started.

Looking at the files exported to the zip archive, the files are named as a combination of the GUID and the filename, so they are at least identifiable.

![File list][filelist]

But the hierarchical relationship is not immediately obvious:

![BSP list][bsplist]

Basically all I really wanted is a way to extract the files out of a BSP application (assuming it has no ABAP events embedded) and be able to easily recreate as a standard web page.

Worth A Feature Request?
========================

In theory it should be straight forward to achieve the above (I'd even be keen to have a go at coding it myself), however I accept it is a fairly niche use-case. In the days before UI5 I doubt there would have been too many customers building fully-fledged web applications and hosting them on a Netweaver stack, as opposed with building a web dynpro/FPM or BSP application.

There may be other examples along a similar line though, for example extracting objects from the MIME repository.

In the meantime doing individual downloads of each file has done the job so it might not even be worth revisiting, however it would be interesting to know if any other customers would find this useful.

Recently Completed
==================

  - Migration of the above apps SAP Cloud Platform (completed the SSL configuration for the custom domain - DNS changes next week)
  - Implemented some configurable custom UI5 application Cache Buster logic using badi /UI5/BADI_CONFIG_HTTP_HANDLER, as per this [OSS note][note]

Up Next
=======

  - Fiori app for producing Customer Quotes/Estimates
  - Small enhancements for Fiori Procurement apps



[angular]: https://egghead.io/technologies/angular2
[tmg]: https://tmgblog.richardhicks.com/forefront-tmg/
[scp]: https://cloudplatform.sap.com/
[abapgit]: https://github.com/larshp/abapGit/
[objectlist]: /images/2017-04-19/001.png "ABAP Git Object List"
[filelist]: /images/2017-04-19/003.png "File List"
[bsplist]: /images/2017-04-19/002.png "BSP file listing"
[note]: https://launchpad.support.sap.com/#/notes/2075016
