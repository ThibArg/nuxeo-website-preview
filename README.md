# nuxeo-website-preview

**WARNING: DO NOT USE THIS REPOSITORY (2015-08)**
It has been cloned and is maintained [here](https://github.com/nuxeo-sandbox/nuxeo-website-preview).
 
 
<hr>
The plug-in provides a widget which displays the preview of a mini-site, where an .html file is displayed, referencing images and resources with _relative_ paths.

It assumes the current document:

* Is a `Folderish`
* And it contains _at its first level_:
  * One single .html file
  * Or, if several, one whose name is `index.html`

If the folder contains several Document whose blobs are html files, it returns one of them (arbitrary), so it is likely the site will not work correctly in this case.

## Good to Know
* it is a _preview_ of the html and its related resources: Related links will all request a resource from the nuxeo server. It is ok for any resurce stored in the correct folder/subfolder, but links will not work with custom and dynamic URLS.

* This works using a _WebEngine_ module whose name in the URLs is `WSP` (**W**eb**S**ite**P**review). Which means the url.

* Also, to be a bit more user friendly, the main url must ends with `index.html`, _whatever_ the real name of your main html file.

* So, to access the preview(*), the URL to use is:

    `{server:port}/nuxeo/site/WSP/main-parent-doc-id/index.html`

For example, say you have a _Folderish_ document, named "My Site", whose `id` is `1234-5678-9ABC-DEF0`, a,nd you are testing on your localhost, you can display the preview using this URL: `http://localhost:8080/nuxeo/site/1234-5678-9ABC-DEF0/index.html`

(*) Assuming vcurrent user is logged in and has enough rights to at least _read_ the blobs), or is anonymous and you allowed anonymous users and setup the permissions, etc. etc.



## Usage

After installing the plug-ins in the server (see below) you must use the specific preview widget deployed by the plug-in. Typically, we recommend doing the following in Nuxeo Studio:

* Create a new Tab, title "Preview" for example
* In the "Activation" sub tab:
  * Make it available only for document with the "Folderish" facet
  * We also recommend you add the following expression in the "Custom EL expression" part: `#{websitePreview.hasMiniSite()}`. This will make sure the "Preview" tab is not displayed when a folder does not contain any html file.
* Drop a "Template" widget
  * In "Custom Properties Configuration", add a new property"
  * Name:  `template`
  * Value: `/widgets/website-preview-widget.xhtml`

Nothing more to do.

## WARNING

The project depends on `nuxeo-fsexporter`, so you must first get it. If, when compiling `nuxeo-website--preview`, you have a dependeny error, then it means you must first clone and `mvn clean install` nuxeo-fsexporter locally.

`nuxeo-fsexporter` should be available in public maven repositories and as a Marketplace Package, but it sometime is not avilable in all and every FastTrask versions.

Current version of `nuxeo-website-preview` uses `nuxeo-fsexplorer` 7.4-SNAPSHOT (since we don't have a 7.3 version), which is ok.

## License
(C) Copyright 2015 Nuxeo SA (http://nuxeo.com/) and others.

All rights reserved. This program and the accompanying materials
are made available under the terms of the GNU Lesser General Public License
(LGPL) version 2.1 which accompanies this distribution, and is available at
http://www.gnu.org/licenses/lgpl-2.1.html

This library is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU
Lesser General Public License for more details.

Contributors:
Thibaud Arguillere (https://github.com/ThibArg)

## About Nuxeo

Nuxeo provides a modular, extensible Java-based [open source software platform for enterprise content management](http://www.nuxeo.com) and packaged applications for Document Management, Digital Asset Management and Case Management. Designed by developers for developers, the Nuxeo platform offers a modern architecture, a powerful plug-in model and extensive packaging capabilities for building content applications.
