## Getting the code

`git clone https://github.com/gshaw-pivotal/repo-monitor.git`

## Setting up to monitor a forked repo

Before deploying you will need to add your particular details to the repo-mon.html file.

1. Complete the compare request specifying your org, forked repo and branch and the upstream repo and branch:

`https://api.github.com/repos/your-org/your-repo/compare/your-branch...upstream-repo:upstream-branch?access_token=`

where 'your-org' is replaced to specify your org as on Github

where 'your-repo' is replaced to specify your repo which is the fork

where 'your-branch' is replaced to specify the branch in your repo that is to be compared

where 'upstream-repo' is replaced to specify the name of the repo you forked from

where 'upstream-branch' is replaced to specify the name of the branch in the upstream repo to compare against

add you Github access token at the end of the request.

2. Complete the branch request to specify the upstream org, repo and branch you want the latest commit from:

`https://api.github.com/repos/upstream-org/upstream-repo/branches/upstream-branch?access_token=`

where 'upstream-org' is replaced to specify the org containing the repo you forked from

where 'upstream-repo' is replaced to specify the name of the repo you forked from

where 'upstream-branch' is replaced to specify the name of the branch in the upstream repo to get the latest commit of

add you Github access token at the end of the request.

3. Complete the commits status request to specify the upstream org and repo containing the commit you want the status of:

`https://api.github.com/repos/upstream-org/upstream-repo/commits/" + branch_sha + "/status?access_token=`

where 'upstream-org' is replaced to specify the org containing the repo you forked from

where 'upstream-repo' is replaced to specify the name of the repo you forked from

where 'branch_sha' is a variable holding the sha of the commit whose status is being checked, it is populated by the previous request and does not need to be modify by a user

add you Github access token at the end of the request.

4. Give the monitor a code name to display be replacing:

`<div align="center" style="font-size:300px">Your project name</div>`

replacing the text 'Your project name' with your code name

## Setting up to monitor PR

Before deploying you will need to add your particular details to the pr-mon.html file.

1. Complete the pulls merge endpoint request, by specifying the upstream org, repo and PR id:

`https://api.github.com/repos/upstream-org/upstream-repo/pulls/" + pr_id + "/merge?access_token=`

where 'upstream-org' is replaced to specify the org of the repo you want to monitor the PRs of

where 'upstream-repo' is replaced to specify the name of the repo you want to monitor the PRs of

where 'pr_id' is a variable populated by a user define string array and is used to identify the PRs that a user cares about.

add you Github access token at the end of the request.

2. Specify the ids of the PRs to be monitored:

This is done by adding the PR ids as strings to the array called 'pr_id_list'.

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
