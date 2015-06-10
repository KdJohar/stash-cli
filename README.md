# pystash
A command-line client for Atlassian Stash written in Python which uses Stash Web API.

## Features
* Git support.
* Support for multiple projects.
* Initiate pull-requests using predefiend templates which can also be used for DoD (Definition of Done) against developer tasks.

Git 1.7.0 or newer
It should also work with older versions, but it may be that some operations involving remotes will not work as expected.

## Setup
### Install python dependancies
pip install click stashy colorama gitpython

### Install pystash

* Get the latest pystash source
`wget https://github.com/purinda/pystash/archive/master.zip

* Unzip master.zip to the directory where you keep additional apps.
`unzip master.zip -d ~/apps/pystash`

* `cd` into the project that you have configured to use pystash (refer to Configure section), create a branch, commit your work
then push it up to the origin repository which pystash is pointed at as well. Then run `~/apps/pystash/pystash.py` to automatically
create the pull-request interactively using pystash.

* [Optional] You can run pystash as a git command by adding a symlink to the `pystash.py` file within your bin directory with
the git command naming convention.
> for an example: if you had a bin directory in your home (~/bin) which is sourced using your .bash_profile then adding a symlink using the command `ln -s ~/apps/pystash/pystash.py ~/bin/git-pystash` let you run pystash by typing `git pystash` or `git-pystash`. (You may need to restart your terminal after doing so or re-source the .bash_profile).

### Configure
pystash uses its own settings section within the .git/config file of the project. Therefore you may need to edit the
.git/config of the git repo you need to use with pystash and place following settings with the parameters from your
stash configuration.

```
[pystash]
    url = http://stash-server-url:7990
    username = demo
    password = demo
    project = acme-project
    repo = acme-desktop-app
    reviewers = john.doe,jane.doe
    template = .pystash.tpl
```

#### Templates
Where **template** key in config above should point to a file within the project directory. Example (.pystash.tpl) template is shown below
```
Covers:
    http://jira.acme.com/browse/PROJ-{{Ticket ID}}
UAT:
    http://{{UAT Name}}.uat.acme.com

{{Solution Description}}

- [ ] Work reflects requirements
- [ ] Docs
- [ ] Tests
- [ ] Product sign off
```
Above template has multiple variables that will be prompted to be filled in before pull-request is initiated.
