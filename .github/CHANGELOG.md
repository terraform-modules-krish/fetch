# Changelog


# v0.4.6
_Released Apr 20, 2023_
## What's Changed
* Update CODEOWNERS by @yorinasub17 in https://github.com/gruntwork-io/fetch/pull/112
* Refactored contexts by @eak12913 in https://github.com/gruntwork-io/fetch/pull/114
* Fixes Go's net-package vulnerability with patched Go version and updated `go-commons` by @oredavids in https://github.com/gruntwork-io/fetch/pull/116

## New Contributors
* @eak12913 made their first contribution in https://github.com/gruntwork-io/fetch/pull/114
* @oredavids made their first contribution in https://github.com/gruntwork-io/fetch/pull/116

**Full Changelog**: https://github.com/gruntwork-io/fetch/compare/v0.4.5...v0.4.6
<br>

# v0.4.5
_Released Aug 3, 2022_
#110  `fetch` should now print an error message if the GitHub release doesn't exist 

<br>

# v0.4.4
_Released Jan 29, 2022_
#103: Fetch now supports outputting the contents of a release asset to standard output so it can be piped to another program.
<br>

# v0.4.3
_Released Jan 24, 2022_
#102 Fixes issues with downloading release assets with names containing regex characters
<br>

# v0.4.2
_Released Mar 29, 2021_
https://github.com/gruntwork-io/fetch/pull/95: Update the build to publish Darwin / ARM 64 binaries that work with the new ARM-based Macs.
<br>

# v0.4.1
_Released Feb 5, 2021_
#92: Fixed the usage help text for `--ref`. 
<br>

# v0.4.0
_Released Feb 5, 2021_
#90: Added a proper logger to `fetch`. It defaults to `INFO`, but the desired verbosity can be specified with `--log-level`. Fixes #89 and #30.
<br>

# v0.3.9
_Released May 4, 2020_
https://github.com/gruntwork-io/fetch/pull/62: This rolls back the change from `v0.3.6`. This means that you can now pass empty values again to `--branch`, `--tag`, and `--commit`, as long as one of those is non-empty, and `fetch` will handle it correctly. 

Special thanks to @vedala for the fix!
<br>

# v0.3.8
_Released Apr 27, 2020_
https://github.com/gruntwork-io/fetch/pull/61: You can now specify an optional `--progress` flag to have `fetch` show progress during downloads. This is especially useful for large downloads.

Special thanks to @ohlsont for the PR!
<br>

# v0.3.7
_Released Sep 10, 2019_
https://github.com/gruntwork-io/fetch/pull/56: Fix the `--source-path` argument to only download the exact paths/files specified. 
<br>

# v0.3.6
_Released Aug 30, 2019_
#31: When fetch is called with `--branch`, `--tag`, `--commit`, a valid error message is now given.

Special thanks to @vedala for the fix!
<br>

# v0.3.5
_Released Apr 19, 2019_
#52: Fixed #48. GitHub Enterprise users can now successfully download binaries.
<br>

# v0.3.4
_Released Mar 4, 2019_
#51 Publish checksums along with binaries.
<br>

# v0.3.3
_Released Feb 20, 2019_
https://github.com/gruntwork-io/fetch/pull/50

Release assets can now be identified using regex. If multiple assets match the regex, `fetch` will automatically download all of them. You can also now pass in multiple checksums, only allowing the download if the computed checksum matches any of the provided ones.

Special thanks to @coryvirok for the contribution!
<br>

# v0.3.2
_Released Oct 12, 2018_
https://github.com/gruntwork-io/fetch/pull/44: Update dependencies from `github.com/codegangsta/cli` to its new name, `gopkg.in/urfave/cli.v1`. There should be no change in behavior.
<br>

# v0.3.14
_Released Feb 3, 2021_
#87: Previously added `--ref` feature broke `--branch` due to conditional ordering
<br>

# v0.3.13
_Released Jan 29, 2021_
https://github.com/gruntwork-io/fetch/pull/85: `fetch` should now properly handle pagination for tags, so you'll be able to fetch older tags from repos that have many tags.
<br>

# v0.3.12
_Released Jan 13, 2021_
#81: Delete circleci nightly job
#79: `fetch` now supports a flexible `--ref` in addition to `--commit`, `--branch`, or `--tag`
<br>

# v0.3.11
_Released Oct 28, 2020_
https://github.com/gruntwork-io/fetch/pull/66: `fetch` will now log the file count after extraction.
https://github.com/gruntwork-io/fetch/pull/77: `fetch` will now skip Git tags that don't follow SemVer. This allows you to use it with repos that use both SemVer and non-SemVer tags.

Special thanks to @pete0emerson for the contributions!
<br>

# v0.3.10
_Released Aug 1, 2020_
https://github.com/gruntwork-io/fetch/pull/70 : fetch now uses go modules instead of `dep` to manage dependencies.
<br>

# v0.3.1
_Released Sep 11, 2018_
https://github.com/gruntwork-io/fetch/pull/36: Fetch should now work with two-digit versions (`vX.Y`).
<br>

# v0.3.0
_Released Aug 11, 2018_
https://github.com/gruntwork-io/fetch/pull/43: `fetch` should now work with GitHub Enterprise URLs! If the repo URL you specify is not GitHub.com, `fetch` will automatically assume it's GitHub Enterprise and use the proper API calls. This defaults to GitHub Enterprise version `v3`, but that can be overridden with the new `--github-api-version` option.
<br>

# v0.2.0
_Released Feb 23, 2018_
#34: Fetch now supports verifying the checksum of a release asset using SHA256 or SHA512. 

Unfortunately, this release also constitutes a breaking change in that `--release-asset` may no longer be passed multiple times. 
<br>

# v0.1.1
_Released Feb 24, 2017_
- https://github.com/gruntwork-io/fetch/pull/23: `fetch` will now exit with a proper error message if you specify an unsatisfiable tag constraint.

<br>

# v0.1.0
_Released Dec 20, 2016_
- We've updated our CI build job to use Go 1.7.3. Before, we were using Go 1.6.x, which apparently [does not work with the latest version of OS X](https://golang.org/doc/go1.7#ports). 

<br>

# v0.0.9
_Released Jun 20, 2016_
- Fix how version number is handled in fetch

<br>

# v0.0.8
_Released Jun 20, 2016_
- Switch to module-ci for build & test

<br>

# v0.0.7
_Released Jun 20, 2016_
- Change build environment to try to get working binaries

<br>

# v0.0.6
_Released Jun 20, 2016_
- Add support back in for reading source paths from command-line args for backwards compatibility

<br>

# v0.0.5
_Released Jun 20, 2016_
- Added support to fetch for downloading not only the source code from a GitHub repo, but also binary assets uploaded to a GitHub release. Downloading such assets is easy for public repos (just `curl` or `wget` the public URL), but for private repos, it's a confusing process that requires multiple API calls. Now, with fetch, it's a one-liner: just use the `--release-asset` option to specify which assets to download.
- This means that instead of reading in the source files to download as an (optional) argument, fetch now uses the `--source-path` argument, which you can specify more than once.
- Added support for reading the GitHub token as the environment variable `GITHUB_OAUTH_TOKEN`. This is more secure than passing it as a command line option.

<br>

# v0.0.4
_Released Jun 4, 2016_
- Fix panic when downloading from a repo that has no tags

<br>

# v0.0.3
_Released Apr 29, 2016_
- fetch can now download files from a specific git commit or a git branch. When a branch is specified, fetch downloads the latest commit on a branch.
- Fixed a bug where empty values for `--tag` were not handled properly for repos whose tag names started with `v`.
- Enables fetch to pull from a specific git commit or branch
- Updated README.md.

<br>

# v0.0.2
_Released Apr 27, 2016_
- Fixes #2. 
- Refined command-line output.

<br>

# v0.0.10
_Released Dec 17, 2016_
- `fetch` now supports tags that don't follow the standard SemVer pattern (MAJOR.MINOR.PATCH), although you cannot use the tag constraint operators (e.g. ~, >, <) with it.

<br>

# v0.0.1
_Released Apr 21, 2016_
Initial release!

<br>

