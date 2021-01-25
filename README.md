# gitlab-clone-all

Simple script to clone all GitLab projects (repos) found in a group and its sub-groups

Uses <https://pypi.org/project/python-gitlab/> for a gitlab CLI command

Install: pip install python-gitlab   # or other mechanisms

Configure a Personal Access Token in GitLab

Create a configuration file, ~/.python-gitlab.cfg, example:

```ini
    [global]
    default = gitlab
    ssl_verify = true
    timeout = 20

    [gitlab]
    url = https://gitlab.com
    private_token = <redacted>
    api_version = 4
```

Look up the GitLab group id, an integer, at the website. Either give that on the command line or you will be prompted for it.

Challenging part: some GitLab repos may be defined as wiki only, and for these the ssh url and local path must change. I was trying to find a way to easily identify this and all I could come up with is that a repo with the metadata value: *empty_repo: True* may be a wiki only. This script will attempt to clone the wiki repo in that case, and if it fails, it will try the regular (empty) repo.

Execute the gitlab-clone-all script with "-h" or "--help" to find out the potential arguments for handling archived repositories and replicating the hierarchy of group/projects/repos found on GitLab.

Kevin Buchs  
New Context Services  
January 25, 2021
