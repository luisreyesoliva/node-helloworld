ibmcloud-hello-node
================================================================================

A "Hello World" server in node.js sample for IBM Cloud.

This repo contains a complete sample of a node.js program that you can deploy
on IBM Cloud (https://cloud.ibm.com/), which is based on
the [Cloud Foundry open source project](http://cloudfoundry.org/).

Before jumping into the code, make sure you have an IBM ID, 


privacy notice
--------------------------------------------------------------------------------

This web application includes code to track deployments to [IBM Bluemix](https://www.bluemix.net/) and other Cloud Foundry platforms. The following information is sent to a [Deployment Tracker](https://github.com/cloudant-labs/deployment-tracker) service on each deployment:

* Application Name (`application_name`)
* Space ID (`space_id`)
* Application Version (`application_version`)
* Application URIs (`application_uris`)

This data is collected from the `VCAP_APPLICATION` environment variable in IBM Bluemix and other Cloud Foundry platforms. This data is used by IBM to track metrics around deployments of sample applications to IBM Bluemix to measure the usefulness of our examples, so that we can continuously improve the content we offer to you. Only deployments of sample applications that include code to ping the Deployment Tracker service will be tracked.

### disabling deployment tracking

Deployment tracking can be disabled by removing the `require("cf-deployment-tracker-client").track();` line from the end of the `server.js` file.

files in this repository
--------------------------------------------------------------------------------

`server.js`

The server written with node.js.  This server was adapted from the
*[example provided in the node docs](http://nodejs.org/api/synopsis.html)*.

The difference is that the port, binding host, and url are determined
via the [`cfenv` package](https://www.npmjs.org/package/cfenv).  This will
return appropriate values both when running in Cloud Foundry and when running
locally.

---

`.cfignore`

List of file patterns that should **NOT** be uploaded to Bluemix.

See the Cloud Foundry doc
*[Prepare to Deploy an Application](http://docs.cloudfoundry.org/devguide/deploy-apps/prepare-to-deploy.html)*
for more information.

In this case, the contents of the file are:

    node_modules

This indicates the node modules you installed with `npm install` will **NOT** be
uploaded to Bluemix.  When your app is "staged" (ie, built on Bluemix during
`cf push`), an
`npm install` will be run there to install the required modules.  By avoiding
sending your node modules when you push your app, your app will be uploaded
quicker than
if you **HAD** sent the modules.  But you can send the modules you have installed
if you like; just delete the `.cfignore` file.

---

`.gitignore`

List of file patterns that should **NOT** be stored in git.  If you aren't using
git, you don't need this file.  And the contents are personal preference.

See the npm google groups topic
*['node_modules in git' from FAQ](https://groups.google.com/forum/#!topic/npm-/8SRXhD6uMmk)*
for discussion.

---

`LICENSE`

The open source license for this sample; in this case, it's licensed under
[Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0).

---

`manifest.yml`

This file contains information that's used when you `cf push` the application.

See the Cloud Foundry doc
*[Deploying with Application Manifests](http://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html)*
for more information.

---

`package.json`

Standard package.json file for node packages.  You will need this file for two
reasons:

* identify your node package dependencies during `npm install`
* identify to Bluemix that this directory contains a node.js application

See the npm doc
*[package.json](https://npmjs.org/doc/json.html)*
for more information.

---

`Procfile`

Used to indicate the command to start the server.

See the Cloud Foundry doc
*[Tips for Node.js Applications](http://docs.cloudfoundry.org/buildpacks/node/node-tips.html)*
and the Heroku doc
*[Process Types and the Procfile](https://devcenter.heroku.com/articles/procfile)*
for more information.

In this case, the file has a single line:

    web: node server

This indicates that the command `node server` should be run when the app is
started.

---

`README.md`

This file!
