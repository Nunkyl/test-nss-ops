# Mirror repo to GitLab

This repo contains a reusable Github Actions workflow that mirrors the current repo to GitLab.

To use it for mirroring a new repo:
- Manually create a corresponding empty repo in GitLab

- Delete the `main` branch in the new repo (make it unprotected first)

- Manually clone the repo from GitHub:
```
git clone --mirror <github_repo_web_URL>
cd <repo_name>.git
git push --mirror <gitlab_repo_web_URL>
```

- Set secrets `GITLAB_USER` and `GITLAB_PASSWORD` in your GitHub repo 

- In the GitHub repo create `.github/workflows/mirror_repo_to_gitlab.yml` with the following content:
```
name: Mirror repo to GitLab

on: [push, pull_request, delete]

jobs:
  call-nss-ops-mirror-workflow:
    uses: Nunkyl/test-nss-ops/.github/workflows/mirror-repo.yml@main
    with:
      GITLAB_URL: <gitlab_repo_web_URL>
    secrets:
      GITLAB_USER: ${{ secrets.GITLAB_USER }}
      GITLAB_PASSWORD: ${{ secrets.GITLAB_PASSWORD }}
```

- Make sure to set the `GITLAB_URL` var

 
Every push to the repo will trigger the action, it will automatically synchronize commits and branches.
PRs, issues and wikis will NOT be mirrored.

Test test test
