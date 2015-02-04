# Welcome to Documentation for Tantalim


## Overview

Learn how to create feature-rich, legacy-friendly, web-powered applications in a fraction of time it takes using
traditional software developers.

### Social

<iframe src="http://ghbtns.com/github-btn.html?user=tantalim&type=follow&size=large" allowtransparency="true"
    frameborder="0" scrolling="0" width="255" height="30"></iframe>

[Discussions on Google+](https://plus.google.com/u/1/explore/Tantalim) [![asdf](img/google-plus-icon.png)
](https://plus.google.com/u/1/explore/Tantalim)

Q&A will be done on [StackOverflow](http://stackoverflow.com/) in the future. TODO - Need someone with
[1500+ reputation](http://stackoverflow.com/help/privileges/create-tags) to create a tag for `tantalim`.

## Architecture

### [Page Layer](pages/)

Rich functionality, custom scripts, and business logic.

### [Model Layer](models/)

Security. Join across multiple tables using one-to-many relationships, many-to-one relationships, or both.

### Table Layer

Tantalim's advanced ORM and rich meta data.

### Database

Relational databases such as MySQL, Oracle and SQL Server. Coming later, No SQL databases such as MongoDB and Cassandra.

### Page Flow

* Browser
    * GET http://localhost:3000/page/BuildTable/ (cacheable only for anonymous use)
    * tantalim-server
        * [`server.js`](https://github.com/tantalim/tantalim-server/blob/master/server.js)
        * [`routes/index.js`](https://github.com/tantalim/tantalim-server/blob/master/app/routes/index.js)
        * [`controllers/pageControllers.js`](https://github.com/tantalim/tantalim-server/blob/master/app/controllers/pageController.js)
         `desktop()`
            * [`views/desktop.html`](https://github.com/tantalim/tantalim-server/blob/master/app/views/desktop.html)
                * Very lightweight shell, besides the need for future security, this could be done 100% client side
* Browser (HTML)
    * GET http://localhost:3000/page-definition/BuildTable (cacheable)
    * tantalim-server
        * [`server.js`](https://github.com/tantalim/tantalim-server/blob/master/server.js)
        * [`routes/index.js`](https://github.com/tantalim/tantalim-server/blob/master/app/routes/index.js)
        * [`controllers/pageControllers.js`](https://github.com/tantalim/tantalim-server/blob/master/app/controllers/pageController.js)
         `pageDefinition()`
            * [`services/pageService.js`](https://github.com/tantalim/tantalim-server/blob/master/app/services/pageService.js)
            * [`services/modelService.js`](https://github.com/tantalim/tantalim-server/blob/master/app/services/modelService.js)
            * [`page/pageDefinition.js`](https://github.com/tantalim/tantalim-server/blob/master/app/views/page/pageDefinition.js)
                * Compiled JavaScript for the custom model and the page objects. This is the "Tantalim bytecode" that
                is used to generate the pages.

* Browser (AngularJS)
    * /lib/tantalim-client/public/js/tantalim-desktop.js (cacheable)
        * [`tantalim.desktop.$routeProvider`](https://github.com/tantalim/tantalim-client/blob/master/public/js/page/main.js)
            * GET http://localhost:3000/page/BuildTable/html (cacheable)
            * tantalim-server
                * [`server.js`](https://github.com/tantalim/tantalim-server/blob/master/server.js)
                * [`routes/index.js`](https://github.com/tantalim/tantalim-server/blob/master/app/routes/index.js)
                * [`controllers/pageControllers.js`](https://github.com/tantalim/tantalim-server/blob/master/app/controllers/pageController.js)
                 `htmlBody()`
                * HTML partial used by AngularJS to display the content.
                    * static HTML content or
                    * [`page/htmlBody`](https://github.com/tantalim/tantalim-server/blob/master/app/views/page/htmlBody.html) partial
                        * [`page`](https://github.com/tantalim/tantalim-server/blob/master/app/views/partials/page.html)
                            * [`html_view`](https://github.com/tantalim/tantalim-server/blob/master/app/views/partials/html_view.html)
                                * [`html_view_single`](https://github.com/tantalim/tantalim-server/blob/master/app/views/partials/html_view_single.html)
        * [`tantalim.desktop.PageController`](https://github.com/tantalim/tantalim-client/blob/master/public/js/page/pageController.js)
            * [`tantalim.common.PageService`](https://github.com/tantalim/tantalim-client/blob/master/public/js/common/pageService.js)
            * [`tantalim.common.ModelCursor`](https://github.com/tantalim/tantalim-client/blob/master/public/js/common/modelCursor.js)
            * [`tantalim.common.ModelSaver`](https://github.com/tantalim/tantalim-client/blob/master/public/js/common/modelSaver.js)
            * [`tantalim.desktop.PageCursor`](https://github.com/tantalim/tantalim-client/blob/master/public/js/page/pageCursor.js)
            * ...and more
            * GET http://localhost:3000/data/BuildTable (dynamic)
            * tantalim-server
                * [`server.js`](https://github.com/tantalim/tantalim-server/blob/master/server.js)
                * [`routes/index.js`](https://github.com/tantalim/tantalim-server/blob/master/app/routes/index.js)
                * [`controllers/dataController.js`](https://github.com/tantalim/tantalim-server/blob/master/app/controllers/dataController.js)
                 `query()`
                    * [`services/dataReader.js`](https://github.com/tantalim/tantalim-server/blob/master/app/services/dataReader.js)
