# [Routing](routing.md)


This page explains the inner workings of FenixEdu CMS's page router.

When routing a request for a page, there are two main components in the page's URL: the site's base URL, and the page's URL within the site.

## Site Router
Each site has its own unique base URL. How this URL is determined depends on whether the site is configured to work standalone, or whether it is associated with a folder.

The router piggy-backs on Bennu Portal, by implementing a PortalBackend, and ensuring that every site is reachable from a functionality. This interaction works differently depending on the site, as described below.

### Standalone

If the site is standalone, (i.e. not associated with a folder), the site's base URL will simply be /<slug>. In this case, the site is directly associated with a MenuFunctionality, thus fully delegating the whole routing process to Portal.



### Folder


When a site is associated with a Folder, the folder is the one associated with a MenuFunctionality, delegating the folder part of the URL to Portal. Then, there are two different ways to resolve the site, depending on the folder's configuration:

+ If the folder has no resolver, the router looks up for a site with a slug matching the path component immediately after the folder's base URL, and returns it if found.
+ If the folder has an associated resolver, site resolution is completely deferred to the resolver.


## Page Router

After the site is resolved, the router strips the site's base URL from the requested URL. This relative URL is split by its path components (i.e. by the / character). If no components are found, and the site has an initial page defined, the initial page is shown. Otherwise, the router looks for a page with a slug matching the first component (this is one of the reasons why slugs cannot have slashes). If one is found, it is displayed. If not, a 'Not Found' page is shown instead.

When displaying a page, the router passes along all the path components, so that the page's rendering logic can access multiple URL parameters, allowing for prettier URLs.


## Static Assets
Static assets for a particular site can be addressed directly under the <site>/static/** path. In the current version, these are the same assets that are defined in the theme, so this method is redundant with the main assets controller, and its usage is discouraged. The router handles these requests directly, simply returning the content from the specified path in the theme's assets.

## RSS Feeds
RSS feeds for each site are available under <site>/rss. These are handled directly by the router, which first extracts the category for which to show the feeds (or none if not provided) and then invokes the feed generator, directly returning its output to the client.