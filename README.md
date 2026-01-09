### Repository to Demo a bug with Dependabot groups

* Related issue reported on the dependabot repo: https://github.com/dependabot/dependabot-core/issues/13154

**Steps to reproduce:**
1. Fork this repository
2. Open the `Actions` tab on your forked version
3. Verify Dependabot has started its update
4. Open the Dependabot update job and read the logs
5. Search for the following snippet in the logs: 
```
2026/01/09 17:51:39 WARN <job_1205057440> Please check your configuration as there are groups where no dependencies match:
- minor-upgrades
- patch-upgrades

This can happen if:
- the group's 'pattern' rules are misspelled
- your configuration's 'allow' rules do not permit any of the dependencies that match the group
- the dependencies that match the group rules have been removed from your project
```
6. Open the Pull Requests and observe that Dependabot correctly opened a pull request for the major-upgrades group but separate pull requests for each dependency that should have been placed in the minor-upgrades group.


**Workaround:**
To workaround this bug you can remove the minor-upgrades group and consolidate all major, minor and patch upgrades into the major-upgrades group OR you can remove the patterns key from each.

**Notes**
* I have not tested patterns that do not contain wildcards

