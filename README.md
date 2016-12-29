# RPM for wp-launch-check

This repository builds an RPM for wp-launch-check.

## Relevant wp-cli RPM names

- wp-cli: Legacy RPM containing wp-cli and wp_launch_check
- wp-cli-0.x: RPM containing only wp-cli (version 0.x)
- wp-launch-check-0.x: RPM containing only wp_launch_check 0.x

The RPM filename built by this repository is:
```
wp-launch-check-0.x-release-0.6.0-01458238016.git4602714.x86_64.rpm
{      name       }-{ type}-{ver}-{iteration}.{ commit }.{arch}.rpm
```
The iteration number is the Circle build number for officiel builds, and a timestamp (seconds since the epoch) for locally-produced builds. The build script will refuse to make an RPM when there are uncommitted changes to the working tree, since the commit hash is included in the RPM name.

## Install Location

This rpm installs:

/opt/pantheon/wp-launch-check-0.x/wp_launch_check.phar

## Releasing to Package Cloud

Any time a commit is merged on a tracked branch, then a WP Launch Check RPM is built and pushed up to Package Cloud.

Branch       | Target
------------ | ---------------
master       | pantheon/internal/fedora/#
Any PR       | pantheon/internal-staging/fedora/#

In the table above, # is the fedora build number (19, 20, 22). Note that WP Launch Check is only installed on app servers, and there are no app servers on anything prior to f22; therefore, at the moment, we are only building for f22.

To release a new version of WP Launch Check, simply update the VERSION.txt file and commit. Run `make` to build locally with docker, or `make with-native-tools` to build without docker. Push to one of the branches above to have an official RPM built and pushed to Package Cloud via Circle CI.

## Provisioning WP Launch Check on Pantheon

Pantheon will automatically install any new RPM that is deployed to Package Cloud. This is controlled by [pantheon-cookbooks/wp-cli](https://github.com/pantheon-cookbooks/wp-cli/blob/master/recipes/default.rb).
