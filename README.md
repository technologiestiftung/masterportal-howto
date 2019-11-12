# masterportal-howto
How to build masterportal instances.

## 1. Get the boilerplate
Download the example boilerplate [here](https://bitbucket.org/geowerkstatt-hamburg/masterportal/downloads/). Do not clone the full repository. Modify the config files: [services.json](https://bitbucket.org/geowerkstatt-hamburg/masterportal/src/03625c9fb2f6f4b19e5c012089a69bfabe789607/doc/services.json.md), [rest-services.json](https://bitbucket.org/geowerkstatt-hamburg/masterportal/src/03625c9fb2f6f4b19e5c012089a69bfabe789607/doc/rest-services.json.md), [style.json](https://bitbucket.org/geowerkstatt-hamburg/masterportal/src/03625c9fb2f6f4b19e5c012089a69bfabe789607/doc/style.json.md). Also feel free to modify the styling of the portal through the css files. 

## 2. Using external services
If you are trying to use wfs/wms/wmts services from another domain, due to cross-origin problems, you will run into problems. The masterportal has its own proxy services. But its a bit tricky to setup depending on the server you are running this on. Therefore, we have created a simple php proxy solution. Get the proxy.php and the .htaccess file from the [repository](https://github.com/technologiestiftung/masterportal-proxy). You don't need to touch the proxy.php, but the .httaccess needs a little modifying. The masterportal translates external urls to proxy requests, e.g *fbinter.stadt-berlin.de* would be translated to *fbinter_stadt-berlin_de*. Therefore, you need to add all external URLs to the .htacces, here is an example:

``
RewriteEngine On

RewriteRule ^fbinter_stadt-berlin_de/(.*)$ /proxy.php?domain=fbinter.stadt-berlin.de&uri=$1 [P,QSA]

RewriteRule ^example-domain_de/(.*)$ /proxy.php?domain=example-domain.de&uri=$1 [P,QSA]
``

If you just need a basic instance, you are done now. If you need further modifications, read on...

## 3. Custom module
If you need a custom module, like our module for the [soziale Einrichtungen](https://github.com/technologiestiftung/masterportal-module-sozialeEinrichtungen), please create a new repository, named "masterportal-module-NAMEofMODULE". Develop the module in there. In order to use your module, you need to build a custom version of the masterportal (see next step).

## 4. Build a custom version of the masterportal
Clone the official [masterportal repository](https://bitbucket.org/geowerkstatt-hamburg/masterportal/src/stable/) on GitHub, make sure you choose the stable branch. Install dependencies `npm install`. In order to test/build your module, you can build a new version of the masterportal by referencing your custom module folder: `npm start -- --CUSTOMMODULE "../MODULE_FOLDER/MODULE"`. Copy the generated files from the *dist* folder to your instance. Done.

## 5. Documentation
There is lots of good [documentation](https://bitbucket.org/geowerkstatt-hamburg/masterportal/src/stable/) on the masterportal for the instance as well as module part.
