***WARNING: THIS REPO IS AN AUTO-GENERATED COPY.*** *This repo has been copied from [Gruntwork’s](https://gruntwork.io/) GitHub repositories so that you can consume it from your company’s own internal Git repositories. This copy is automatically created and updated by the `repo-copier` CLI tool. If you need to make changes to this repo, you should make the changes in a separate fork, and NOT make changes directly in this repo, as otherwise, the `repo-copier` will overwrite your changes! Please see the `repo-copier` [documentation](https://github.com/terraform-modules-krish/repo-copier) for more information on how the code is copied, how cross-references are updated, how the changelog is handled, etc.*

***

_You may find it valuable to view the following resources in the original repo. If these links give you a 404, visit https://app.gruntwork.io to gain access or email support@gruntwork.io if you need assistance._

[Home Page](https://github.com/gruntwork-io/fetch/) |
[Pull Requests](https://github.com/gruntwork-io/fetch/pulls) |
[Issues](https://github.com/gruntwork-io/fetch/issues) |
[Releases and Assets](https://github.com/gruntwork-io/fetch/releases)

_Alternatively, you can view a copied version of the resources listed above._

[Pull Requests](https://github.com/terraform-modules-krish/fetch/blob/master/.github/PULL_REQUESTS.md) |
[Issues](https://github.com/terraform-modules-krish/fetch/blob/master/.github/ISSUES.md) |
[ChangeLog](https://github.com/terraform-modules-krish/fetch/blob/master/.github/CHANGELOG.md)

***

# fetch

fetch will download a file or folder from a specific tag of a GitHub repo, subject to the [Semantic Versioning](http://semver.org/) 
constraints you impose. It works for public repos, and for private repos by allowing you to specify a GitHub [Personal Access Token](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).

It is well-suited to downloading the latest version of a file or folder published in a GitHub repo such that you get 
the latest non-breaking-change version. Basically, it's like a package manager, but for arbitrary GitHub repos.

## Motivation

[Gruntwork](http://gruntwork.io) helps software teams get up and running on AWS with DevOps best practices and world-class 
infrastructure in about 2 weeks. Sometimes we publish scripts that clients use in their infrastructure, and we want clients
to auto-download the latest non-breaking version of a script when we publish updates. In addition, for security reasons,
we wish to verify the integrity of the git commit being downloaded.

## Installation

Download the binary from the [GitHub Releases](https://github.com/gruntwork-io/script-modules/releases) tab. 

## Assumptions

fetch assumes that a repo's tags are in the format `vX.Y.Z` or `X.Y.Z` to support Semantic Versioning parsing. Repos that
use git tags not in this format cannot be used with fetch.

## Usage

#### General Usage

```
fetch --repo=<github-repo-url> --tag=<version-constraint> [<repo-download-filter>] <local-download-path>
```

- `<repo-download-filter>` 
  **Optional**.
  If blank, all files in the repo will be downloaded. Otherwise, only files located in the given path
  will be downloaded. 
  - Example: `/` Download all files in the repo
  - Example: `/folder` Download only files in the `/folder` path and below from the repo
- `<local-download-path>`
  **Required**.
  The local path where all files should be downloaded.
  - Example: `/tmp` Download all files to `/tmp`

Run `fetch --help` to see more information about the flags, some of which are required. See [Version Constraint Operators](#version-constraint-operators)
for examples of version constraints you can use.

#### Example 1

Download `/modules/foo/bar.sh` from a GitHub tagged release where the tag is the latest version of 0.1.x but at least 0.1.5, and save it to `/tmp/bar`:

```
fetch \
--repo="https://github.com/gruntwork-io/script-modules" \
--tag="~>0.1.5" \
/modules/foo/bar.sh \
/tmp/bar
```

#### Example 2

Download all files in `/modules/foo` from a GitHub tagged release where the tag is exactly 0.1.5, and save them to `/tmp`:

```
fetch \
--repo="https://github.com/gruntwork-io/script-modules" \
--tag="0.1.5" \
/modules/foo \
/tmp

```

#### Example 3

Download all files in `/modules/foo` from a private GitHub repo using the GitHUb oAuth Token "123". Get the release whose tag is exactly 0.1.5, and save the files to `/tmp`:

```
fetch \
--repo="https://github.com/gruntwork-io/script-modules" \
--tag="0.1.5" \
--github-oauth-token="123" \
/modules/foo \
/tmp

```

#### Version Constraint Operators

The value of `--tag` can be expressed using any operators defined in [hashicorp/go-version](https://github.com/hashicorp/go-version).

Specifically, this includes:

| Version Constraint Pattern | Meaning                                  |
| -------------------------- | ---------------------------------------- |
| `1.0.7`                    | Exactly version `1.0.7`                  |
| `=1.0.7`                   | Exactly version `1.0.7`                  |
| `!=1.0.7`                  | The latest version as long as that version is not `1.0.7` |
| `>1.0.7`                   | The latest version greater than `1.0.7`  |
| `<1.0.7`                   | The latest version that's less than `1.0.7` |
| `>=1.0.7`                  | The latest version greater than or equal to `1.0.7` |
| `<=1.0.7`                  | The latest version that's less than or equal to `1.0.7` |
| `~>1.0.7`                  | The latest version that is greater than `1.0.7` and less than `1.1.0` |
| `~>1.0`                    | The latest version that is greater than `1.0` and less than `2.0` |

## TODO

- Introduce code verification using something like GPG signatures or published checksums
- Explicitly test for exotic repo and org names
- Apply stricter parsing for repo-filter command-line arg
