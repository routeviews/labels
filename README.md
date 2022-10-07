# GitHub Labels

An Ansible-based solution for syncing GitHub Issue Labels between GitHub Repositories.

> This solution leverages the "github-label-sync" npm packaged tool.

## Dependencies

* `ansible` is used to 
* `npm` must be available

## Example

Run with the `--check` flag to see the Dry Run output, like the following:

    $ ansible-playbook sync-labels.yml  --check
    GitHub Access Token: 
    GitHub Organization or User [routeviews]: 
    Which repository would you like to update? [infra]: frr
    Which repository would you like to retrieve labels from? [labels]: 

    ... omitted for brevity...

    TASK [Dry Run Output] *********************************************************************************************************************
    ok: [localhost] => {
        "dryrun_output.stdout_lines": [
            "Syncing labels for \"routeviews/frr\"",
            "Validating provided labels",
            "Fetching labels from GitHub",
            " > Missing: the \"DNS\" label is missing from the repo. It will be created.",
            " > Missing: the \"email\" label is missing from the repo. It will be created.",
            " > Missing: the \"invalid\" label is missing from the repo. It will be created.",
            " > Missing: the \"security\" label is missing from the repo. It will be created.",
            " > Missing: the \"update dependencies\" label is missing from the repo. It will be created."
        ]
    }

    ... trimmed for brevity...

Run without the `--check` argument to sync the GitHub Issue Labels:

    $ ansible-playbook sync-labels.yml
    GitHub Access Token: 
    GitHub Organization or User [routeviews]: 
    Which repository would you like to update? [infra]: frr
    Which repository would you like to retrieve labels from? [labels]: 

    ... omitted for brevity...

    TASK [Sync output] ************************************************************************************************************************
    ok: [localhost] => {
        "sync_output.stdout_lines": [
            "Syncing labels for \"routeviews/frr\"",
            "Validating provided labels",
            "Fetching labels from GitHub",
            " > Missing: the \"DNS\" label is missing from the repo. It will be created.",
            " > Missing: the \"email\" label is missing from the repo. It will be created.",
            " > Missing: the \"invalid\" label is missing from the repo. It will be created.",
            " > Missing: the \"security\" label is missing from the repo. It will be created.",
            " > Missing: the \"update dependencies\" label is missing from the repo. It will be created."
        ]
    }

    ... trimmed for brevity...

## TODO

- [ ] Enable syncing all repositories within an organization/user.
- [ ] Consider removing `vars_prompt` to enable simply running this in GitHub Action workflow.
- [ ] Consider converting the playbook itself into a GitHub Action.
