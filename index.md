---
layout: default
---

## Why podio-export?

On December 18, 2018 [Podio](https://podio.com/) notified its users of [Upcoming Changes to Podio Free](https://help.podio.com/hc/en-us/community/posts/360034170732-Upcoming-Changes-to-Podio-Free). The announcement came as a surprise to long time Podio users. `podio-export` was put together to help users easily export their data data.

## Is podio-export for me?

You may want to use `podio-export` if you:

-   Simply want to backup your existing Podio data (any type of account).
-   Are looking to backup old Podio data from a free Podio account that you do now plan to use anymore.
-   Are looking to export you data so it can be migrated (imported) elsewhere later.

## What options does podio-export offer?

`podio-export` will offer an [open source Javascript tool](https://github.com/podio-export/podio-export#readme) to export your data (initially into JSON files). See section [`podio-export` Javascript tool -> Data exported)](#data-exported) for details.

If there is enough interest, we may offer a simple webpage where a user would provide a [Podio client_id and client_secret](https://podio.com/settings/api) as well as their Podio username and password and be able to export their data straight into a Google Drive account. Please [let us know](https://github.com/podio-export/podio-export/issues/1) in case you are unable to use the tool and might require a webpage instead.

## Data exported

The following describes which data is exported by the [`podio-export`](https://github.com/podio-export/podio-export#readme) tool:

-   For the user account provided, will export data for each organization as follows:
    -   `./podio-export/USER_NAME/summary.json` contains a count of all data exported in the last `podio-export` session.
    -   `./podio-export/USER_NAME/contacts_X-Y.json` files containing contacts X through Y for user `USER_NAME`.
    -   `./podio-export/USER_NAME/ORG_NAME` folder (one for each organization).
    -   `./podio-export/USER_NAME/ORG_NAME/ORG_NAME.json` file containing information about organization `ORG_NAME`.
    -   `./podio-export/USER_NAME/ORG_NAME/tasks_X-Y.json` files containing tasks X through Y for organization `ORG_NAME`.
-   For each organization identified, will export data for each workspace as follows:
    -   `./podio-export/USER_NAME/ORG_NAME/WORKSPACE_NAME`: folder (one for each workspace).
    -   `./podio-export/USER_NAME/ORG_NAME/WORKSPACE_NAME/WORKSPACE_NAME.json` file containing information about workspace `WORKSPACE_NAME`.
-   For each workspace identified, will export data for each workspace as follows:
    -   `./podio-export/USER_NAME/ORG_NAME/WORKSPACE_NAME/APP_NAME`: folder (one for each application).
    -   `./podio-export/USER_NAME/ORG_NAME/WORKSPACE_NAME/APP_NAME/APP_NAME.json` file containing information about application `APP_NAME`.
    -   `./podio-export/USER_NAME/ORG_NAME/WORKSPACE_NAME/APP_NAME/items_X-Y.json` files containing items X through Y for application `APP_NAME`.
    -   `./podio-export/USER_NAME/ORG_NAME/WORKSPACE_NAME/APP_NAME/files_X-Y.json` files containing information on files X through Y in application `APP_NAME`.
    -   `./podio-export/USER_NAME/ORG_NAME/WORKSPACE_NAME/APP_NAME/files` folder containing the actual files in application `APP_NAME`.

## Rate limiting & performance

Please note that Podio will [rate limit](https://developers.podio.com/index/limits) requests and lower rate limits apply for the following `podio-export` actions:

-   Exporting organization tasks (each 100 tasks exported count as one request).
-   Exporting application items (each 500 items of a single app exported to JSON count as one request).
-   Downloading files (each file downloaded counts as one request).

In order to work within these rate limits, once the limit is reached `podio-export` will halt and wait until the next rate interval (hour) to continue working.
