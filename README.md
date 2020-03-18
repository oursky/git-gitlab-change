# Simple script for checking is a sub path have changes in a Gitlab CI PR build

For travis-ci, you may checkout the sister project: https://github.com/oursky/git-travis-change

## Usage

```
source <(curl https://raw.githubusercontent.com/oursky/git-gitlab-change/master/install)
git travis-change andoird ./script/test-android.sh
```

## Example gitlab-ci.yml

```
before_install:
  - curl https://raw.githubusercontent.com/oursky/git-gitlab-change/master/install | bash
script:
  - git gitlab-change backend script/build-backend.sh
```

# Objective of the script

When we have multiple project in same repo and use matrix/stage to build for
testing, there might be chance building a folder again that have no change.

For example, we have following folder:

```
ios/
web/
skygear/
```

Changes are often only happen in one sub-folder. i.e. PR changing ios code
will not likely to change the web code.

Although running all test against any line of change does not hurt, but in
reality the resource is limited and we want to make good use of them.

This script is intended to make the checking easy while the making the build
script is still local runnable.

