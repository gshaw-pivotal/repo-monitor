## Getting the code

`git clone https://github.com/gshaw-pivotal/repo-monitor.git`

## Setting up to monitor a forked repo

Before deploying you will need to add your particular details to the repo-mon.html file.

1. Specify your forked repo, replacing the following:

`your-org/your-repo/compare/your-branch`

where 'your-org' is replaced to specify your org as on Github
where 'your-repo' is replaced to specify your repo which is the fork
where 'your-branch' is replaced to specify the branch in your repo that is to be checked

2. Specify the original repo from which you forked, replacing the following:

`upstream-repo:upstream-branch`

where 'upstream-repo' is replaced to specify the name of the repo you forked from
where 'upstream-branch' is replaced to specify the branch of the repo you forked from to be compared against

3. Specify you Guthub API access token by adding it at the end:

`?access_token=`

4. Give the monitor a code name to display be replacing:

`<div align="center" style="font-size:300px">Your project name</div>`

replacing the text 'Your project name' with your code name

## Setting up to monitor PR

Before deploying you will need to add your particular details to the pr-mon.html file.

1. Specify the repo to monitor the status of PRs, by replacing the following:

`upstream-org/upstream-repo`

where 'upstream-org' is replaced to specify the org of the repo you want to monitor the PRs of
where 'upstream-repo' is replaced to specify the name of the repo you want to monitor the PRs of

2. Specify you Guthub API access token by adding it at the end:

`?access_token=`

3. Specify the ids of the PRs to be monitored:

This is done by adding the ids as strings to the array called 'pr_id_list'.

```
//List of PR ids as strings
const pr_id_list = [''];
```

## Deploying

This monitor can be deployed to cloudfoundry as a static application using the static buildpack. This an be achieved with the following command issued in the root directory of this repo:

`cf push app-name`

## Limitations

As this uses the static buildpack, the application will not have access to cloudfoundry environment variables.

Also, if your list of PRs being monitored changes, you will need to update the appropriate variable and then redeploy the application to cloudfoundry. Afterwards, any browser displaying the pr-mon.html page will need to be refreshed to get the latest list of PRs.

## Credits

Credit to TheBoysAreZachInTown for the first version of the repo-mon file and script.
