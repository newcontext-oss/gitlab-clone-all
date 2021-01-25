# gitlab-clone-all

Simple script to clone all GitLab projects (repos) found in a group and its sub-groups

Uses https://pypi.org/project/python-gitlab/ for a gitlab CLI command

Install: pip install python-gitlab   # or other mechanisms

Configure a Personal Access Token in GitLab

Create a configuration file, ~/.python-gitlab.cfg, example:

```ini
    [global]
    default = gitlab
    ssl_verify = true
    timeout = 5

    [gitlab]
    url = https://gitlab.com
    private_token = <redacted>
    api_version = 4
```

Look up the GitLab group id, an integer, at the website. Either give that on the command line or you will be prompted for it.

Challenging part: some GitLab repos may be defined as wiki only, and for these the ssh url and local path must change. I was trying to find a way to easily identify this and all I could come up with is that a repo with the metadata value: *empty_repo: True*. However, this means if you actually have a normal repo that is empty, it will fail to clone that because it tries to clone it as a wiki-only repo.

Kevin Buchs  
New Context Services  
October 30, 2020
