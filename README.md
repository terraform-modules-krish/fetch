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

fetch makes it easy to download files, folders, or release assets from a specific commit, branch, or tag of
a public or private GitHub repo.

#### Motivation

[Gruntwork](http://gruntwork.io) helps software teams get up and running on AWS with DevOps best practices and
world-class infrastructure in about a day. Sometimes we publish scripts and binaries that clients use in their
infrastructure, and we want an easy way to install a specific version of one of those scripts and binaries. While this
is fairly straightforward to do with public GitHub repos, as you can usually `curl` or `wget` a public URL, it's much
trickier to do with private GitHub repos, as you have to make multiple API calls, parse JSON responses, and handle
authentication. Fetch makes it possible to handle all of these cases with a one-liner.

#### Features

- Download from a specific git tag, branch, or commit SHA.
- Download a single file, a subset of files, or all files from the repo.
- Download a binary asset from a specific release.
- Verify the SHA256 or SHA512 checksum of a binary asset.
- Download from public repos, or from private repos by specifying a [GitHub Personal Access Token](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).
- Download from GitHub Enterprise.
- When specifying a git tag, you can can specify either exactly the tag you want, or a [Tag Constraint Expression](#tag-constraint-expressions) to do things like "get the latest non-breaking version" of this repo. Note that fetch assumes git tags are specified according to [Semantic Versioning](http://semver.org/) principles.

#### Quick examples

Download folder `/baz` from tag `0.1.3` of a GitHub repo and save it to `/tmp/baz`:

```
fetch --repo="https://github.com/foo/bar" --tag="0.1.3" --source-path="/baz" /tmp/baz
```

Download the release asset `foo.exe` from release `0.1.5` and save it to `/tmp`:

```
fetch --repo="https://github.com/foo/bar" --tag="0.1.5" --release-asset="foo.exe" /tmp
```

See more examples in the [Examples section](#examples).

## Installation

Download the fetch binary from the [GitHub Releases](https://github.com/gruntwork-io/fetch/releases) tab.

## Usage

#### Assumptions

fetch assumes that a repo's tags are in the format `vX.Y.Z` or `X.Y.Z` to support Semantic Versioning parsing. This allows you to specify a [Tag Constraint Expression](#tag-constraint-expressions) to do things like "get the latest non-breaking version" of this repo. Note that fetch also allows downloading a specific tag not in SemVer format.

#### General Usage

```
fetch [OPTIONS] <local-download-path>
```

The supported options are:

- `--repo` (**Required**): The fully qualified URL of the GitHub repo to download from (e.g. https://github.com/foo/bar).
- `--tag` (**Optional**): The git tag to download. Can be a specific tag or a [Tag Constraint
  Expression](#tag-constraint-expressions).
- `--branch` (**Optional**): The git branch from which to download; the latest commit in the branch will be used. If
  specified, will override `--tag`.
- `--commit` (**Optional**): The SHA of a git commit to download. If specified, will override `--branch` and `--tag`.
- `--source-path` (**Optional**): The source path to download from the repo (e.g. `--source-path=/folder` will download
  the `/folder` path and all files below it). By default, all files are downloaded from the repo unless `--source-path`
  or `--release-asset` is specified. This option can be specified more than once.
- `--release-asset` (**Optional**): The name of a release asset--that is, a binary uploaded to a [GitHub
  Release](https://help.github.com/articles/creating-releases/)--to download. It only works with the `--tag` option.
- `--release-asset-checksum` (**Optional**): The checksum that a release asset should have. Fetch will fail if this value
  is non-empty and does not match the checksum computed by Fetch.
- `--release-asset-checksum-algo` (**Optional**): The algorithm fetch will use to compute a checksum of the release asset.
  Supported values are `sha256` and `sha512`.
- `--github-oauth-token` (**Optional**): A [GitHub Personal Access
  Token](https://help.github.com/articles/creating-an-access-token-for-command-line-use/). Required if you're
  downloading from private GitHub repos. **NOTE:** fetch will also look for this token using the `GITHUB_OAUTH_TOKEN`
  environment variable, which we recommend using instead of the command line option to ensure the token doesn't get
  saved in bash history.
- `--github-api-version` (**Optional**): Used when fetching an artifact from a GitHub Enterprise instance.
  Defaults to `v3`. This is ignored when fetching from GitHub.com.

The supported arguments are:

- `<local-download-path>` (**Required**): The local path where all files should be downloaded (e.g. `/tmp`).

Run `fetch --help` to see more information about the flags.

#### Tag Constraint Expressions

The value of `--tag` can be expressed using any operators defined in [hashicorp/go-version](https://github.com/hashicorp/go-version).

Specifically, this includes:

| Tag Constraint Pattern | Meaning                                  |
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

## Examples

#### Usage Example 1

Download `/modules/foo/bar.sh` from a GitHub release where the tag is the latest version of `0.1.x` but at least `0.1.5`, and save it to `/tmp/bar`:

```
fetch --repo="https://github.com/foo/bar" --tag="~>0.1.5" --source-path="/modules/foo/bar.sh" /tmp/bar
```

#### Usage Example 2

Download all files in `/modules/foo` from a GitHub release where the tag is exactly `0.1.5`, and save them to `/tmp`:

```
fetch --repo="https://github.com/foo/bar" --tag="0.1.5" --source-path="/modules/foo" /tmp
```

#### Usage Example 3

Download all files from a private GitHub repo using the GitHUb oAuth Token `123`. Get the release whose tag is exactly `0.1.5`, and save the files to `/tmp`:

```
GITHUB_OAUTH_TOKEN=123

fetch --repo="https://github.com/foo/bar" --tag="0.1.5" /tmp
```

#### Usage Example 4

Download all files from the latest commit on the `sample-branch` branch, and save them to `/tmp`:

```
fetch --repo="https://github.com/foo/bar" --branch="sample-branch" /tmp/josh1
```

#### Usage Example 5

Download all files from the git commit `f32a08313e30f116a1f5617b8b68c11f1c1dbb61`, and save them to `/tmp`:

```
fetch --repo="https://github.com/foo/bar" --commit="f32a08313e30f116a1f5617b8b68c11f1c1dbb61" /tmp/josh1
```

#### Usage Example 6

Download the release asset `foo.exe` from a GitHub release where the tag is exactly `0.1.5`, and save it to `/tmp`:

```
fetch --repo="https://github.com/foo/bar" --tag="0.1.5" --release-asset="foo.exe" /tmp
```

#### Usage Example 7

Download the release asset `foo.exe` from a GitHub release hosted on a GitHub Enterprise instance running at `ghe.mycompany.com` where the tag is exactly `0.1.5`, and save it to `/tmp`:

```
fetch --repo="https://ghe.mycompany.com/foo/bar" --tag="0.1.5" --release-asset="foo.exe" /tmp
```

## License

This code is released under the MIT License. See [LICENSE.txt](https://github.com/terraform-modules-krish/fetch/blob/v0.3.0/LICENSE.txt).

## TODO

- Introduce code verification using something like GPG signatures or published checksums
- Explicitly test for exotic repo and org names
- Apply stricter parsing for repo-filter command-line arg
