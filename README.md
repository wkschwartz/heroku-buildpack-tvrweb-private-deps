Heroku Buildpack for Installing TVRepack
========================================

TVRepack is currently closed source and as such is a private repo at GitHub.
This makes it difficult to install on a Heroku app without putting your GitHub
password in your app's repo.

Usage
-----

Your app should have [Buildpack
Multi](https://github.com/ddollar/heroku-buildpack-multi). Your `.buildpacks`
file should look like this:

```
https://github.com/heroku/heroku-buildpack-python.git
https://github.com/EconomistsInc/heroku-buildpack-tvrweb-private-deps.git
```

Then create a [GitHub OAuth API
token](https://help.github.com/articles/git-over-https-using-oauth-token):

```bash
$ curl -u "$YOUR_GITHUB_USERNAME" -d '{"scopes":["repo"],"note":"TVRepack"}' https://api.github.com/authorizations | grep token
```

Remember this token and keep it safe like a password. You can always [revoke it
and create a new one](https://github.com/settings/applications).

Set this token in your Heroku app as an environment variable:

```bash
$ heroku config:set GITHUB_OAUTH_TOKEN=$THE_TOKEN_FROM_THE_PREVIOUS_STEP
```

Now you should be ready to provision your app.

```bash
$ git push heroku master
```
