## Description

This program makes it easier to download one or more days of fitbit data via the Fitbit python API.  While Fitbit makes it possible to download up to a month via their website gui (gear icon), this program permits you to do so very quickly, and for many days between start+finish dates.

Output is tab-delimited for easy import into spreadsheets.


## Installation Instructions

### Register an app on dev.fitbit.com

The instructions on fitbit.com are cryptic at best.
This works for me.

```
    Application Name            = whatever you want
    Description                 = whatever you want
    Application Website         = http://localhost
    Organization                = whatever you want
    Organization Website        = http://localhost
    Terms of Service Url        = http://localhost
    Privacy Policy Url          = http://localhost
    Oauth 2.0 Application Type  = Personal              <==== required
    Callback URL                = http://127.0.0.1:8080 <==== required
    Default Access Type         = Read-Only             <==== required
```

### Save your Client ID and Secret

On the 'Applications I registered' page in the section for the app you created above, note your:

```
    OAuth 2.0 Client ID
    Client Secret
```

Copy `config.yml.example` to `config.yml` and edit the values therein to match.

IMPORTANT: treat this file like a private key file.
Do not save it anywhere publically readable such as github.


### Save initial access tokens

Save initial file

* copy `tokens.yml.example` to `tokens.yml`

Tokens are typically good for 8 hours by default.  If you want to save tokens to make a number of runs of this program in a row without having the rather verbose output due to requesting keys every run, run the `gather_keys_oauth2.py` script and edit `tokens.yml` to save the returned values.  See the comments in `tokens.yml` for details.

If you save tokens to `tokens.yml`, subsequent runs of this program will just output the step count for the day(s) specified until the token expires, at which it will revert to the default 'request a new token every run' behavior.

### Install required python libraries
`sudo pip install cherrypy pyaml fitbit`

### Try it out

* get brief usage
`python get-fitbit-steps`

* get more verbose help
`python get-fitbit-steps --help`

* specify a range of dates
`python get-fitbit-steps --begin 2018-01-01 --end 2018-01-31`

* specify one date (set begin+end the same)
`python get-fitbit-steps --begin 2018-01-15 --end 2018-01-15`

### Python version compatibility

* python 2.7 seems to be required by cherrypy (sorry centos-6 users)
* python 2.7 also seems to be required by gather_keys_oauth2.py (copied here from upstream)

### CLI-only notes

Unfortunately `cherrypy` opens a browser windows on localhost, so you cannot currently run this program in a text-only session such as under Vagrant via ssh or the like.

### Acknowledgements

Many thanks to the author of the reference article at:
https://towardsdatascience.com/collect-your-own-fitbit-data-with-python-ff145fa10873

