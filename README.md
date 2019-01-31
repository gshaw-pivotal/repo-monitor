## Getting the code

`git clone https://github.com/gshaw-pivotal/repo-monitor.git`

## Setting up to monitor a forked repo

Before deploying you will need to add your particular details to the repo-mon.html file.

1. Set the following constants:

`your_org` is set to specify your org as on Github

`your_repo` is set to specify your repo which is the fork

`your_branch` is set to specify the branch in your repo that is to be compared

`upstream_org` is set to specify the name of the org you forked the repo from

`upstream_repo` is set to specify the name of the repo you forked from

`upstream_branch` is set to specify the name of the branch in the upstream repo to compare against

`access_token` is set to your Github access token

`update_interval` specifies how often (in milliseconds) the page rechecks with GitHub to keep up to date, with `60000` (1 minute) being the default provided

2. Give the monitor a code name to display be replacing:

`<div align="center" style="font-size:300px">Your project name</div>`

replacing the text 'Your project name' with your code name

## Setting up to monitor PR

Before deploying you will need to add your particular details to the pr-mon.html file.

1. Set the following constants:

`upstream_org` is set to specify the name of the org you forked the repo from

`upstream_repo` is set to specify the name of the repo you forked from

`access_token` is set to your Github access token

`update_interval` specifies how often (in milliseconds) the page rechecks with GitHub to keep up to date, with `60000` (1 minute) being the default provided

2. Specify the ids of the PRs to be monitored:

This is done by adding the PR ids as strings to the array called 'pr_id_list'.

```
//List of PR ids as strings
const pr_id_list = [''];
```

## Basic Authentication

To secure to pages served by the app, include a `Staticfile.auth` when deploying to cloudfoundry. The file will contain username and hashed password pairs, which are used to determine if a client should be granted access to the resource.

A `Staticfile.auth` contents will be structed as follows:

```
USERNAME1:HASHED_PASSWORD
USERNAME2:HASHED_PASSWORD
```

You can use [Htpasswd Generater]([http://www.htaccesstools.com/htpasswd-generator/) to generate the hashed version of the password(s). Do not include plain text passwords in the `Staticfile.auth`.

## Deploying

This monitor can be deployed to cloudfoundry as a static application using the static buildpack. This an be achieved with the following command issued in the root directory of this repo:

`cf push app-name`

## Limitations

As this uses the static buildpack, the application will not have access to cloudfoundry environment variables.

Also, if your list of PRs being monitored changes, you will need to update the appropriate variable and then redeploy the application to cloudfoundry. Afterwards, any browser displaying the pr-mon.html page will need to be refreshed to get the latest list of PRs.

## Credits

Credit to TheBoysAreZachInTown for the first version of the repo-mon file and script.
