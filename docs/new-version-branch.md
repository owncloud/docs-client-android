# Create a New Version Branch for the iOS App

When doing a new release for the iiOS App like `11.x`, a new version branch must be created based on `master`. It is necessary to do this in four steps. Please set the new and former version numbers accordingly

**Step 1: Create and configure the new `11.x` branch**

1.  Create a new `11.x` branch based on latest `origin/master`
2.  Copy the `.drone.star` file from the _former_ `11.x-1` branch
    (it contains the correct branch specific setup rules and replaces the current one coming from master)
3.  In `.drone.star` set `latest_version` to `11.x` (on top in section `def main(ctx)`)
4.  In `site.yml` adjust all `-version` keys according the new and former releases
    (in section `asciidoc.attributes`)
5.  In `antora.yml` change the version from `master` to `11.x`
6.  Run a build by entering `yarn antora-local`. No errors should occur
7.  Commit the changes and push the new `11.x` branch. **DO NOT CREATE A PR!**

**Step 2: Configure the master branch to use the new `11.x` branch**

9.  Create a new `changes_necessary_for_11.x` branch based on latest `origin/master`
10.  In `.drone.star` set `latest_version` to `11.x` (on top in section `def main(ctx)`)
11. In `site.yml` adjust all `-version` keys according the new and former releases
    (in section `asciidoc.attributes`)
12. No changes in `antora.yml` but check if the version is set to `master`
13. Run a build by entering `yarn antora-local`. No errors should occur
14. Commit changes and push it
15. Create a Pull Request. When CI is green, all is done correctly. Merge the PR to master.

**Step 3: Set the correct Desktop build branches in the docs repo**

16. In `site.yml` of [docs](https://github.com/owncloud/docs/blob/master/site.yml) adjust the last **two** branches at `url: https://github.com/owncloud/docs-client-desktop.git` accordingly
    (in section `content.sources.url.branches`)

**Step 4: Protection and Renaming**

17. Go to the settings of the this repository and change the protection of the branch list (Settings > Branches) so that
    the `11.x` branch gets protected and the `11.x-2` branch is no longer protected.
18. Rename the `11.x-2` branch to `x_archived_11.x-2`

