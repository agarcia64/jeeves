# Jeeves

## Purpose
Jeeves is an automated report generator for Jenkins CI. It generates an HTML report using Jinja2 templating and sends it out over email using Python's smtplib.

## Setup
Create a file named "config.yaml" based off "config.yaml.example" with the following fields filled in:
- **jenkins_url**: URL of your Jenkins server
- **jenkins_username**: Your Jenkins username
- **jenkins_api_token**: Your Jenkins API token
- **job_search_field**: Filter of Jenkins Jobs to included in report, e.g. DFG-ceph-rhos
- **bz_url**: URL of your Bugzilla, e.g. https://bugzilla.redhat.com/
- **jira_url**: URL of your Jira, e.g. https://projects.engineering.redhat.com/
- **jira_username**: Your Jira username (note: this field is only required if the tickets you wish to access have restricted view permissions)
- **jira_password**: Your Jira password (note: this field is only required if the tickets you wish to access have restricted view permissions)
- **certificate**: CRT file to authenticate with Jira server
- **smtp_host**: SMTP host of your email
- **email_subject**: Subject of your email report
- **email_to**: Email address you would like to send your report to

If you wish to use a different configuration file, you can specify it as a command line argument.

#### Tracking Blockers
Create a file named "blockers.yaml" based off "blockers.yaml.example" with each UNSTABLE and FAILED job containing two sections - 'bz' and 'jira' - and a list of the blocker IDs. 0 indicates blocker bug/ticket is not on file (either doesn't exist or hasn't been created yet)

If you wish to use a different blockers file, you can specify it as a command line argument.

## Usage
To run:
- `$ ./main.py [optional: --config CONFIG] [optional: --blockers BLOCKERS]` if `/usr/bin/python3` is a valid path
- `$ python3 main.py [optional: --config CONFIG] [optional: --blockers BLOCKERS]` otherwise

### Packages
- [PyYAML](https://pyyaml.org/) for parsing config YAML
- [Jinja2](https://jinja.palletsprojects.com/en/2.10.x/) for generating HTML
- [Python Jenkins](https://python-jenkins.readthedocs.io/en/latest/) for interacting with Jenkins
- [python-bugzilla](https://github.com/python-bugzilla/python-bugzilla) for interacting with Bugzilla
- [jira-python](https://jira.readthedocs.io/en/master/index.html) for interacting with Jira

To install packages run:

`$ pip install -r requirements.txt`

## Testing

Jeeves has a small but growing test suite driven by [pytest](https://docs.pytest.org/en/latest/index.html). Currently all tests reside in the `test_main.py` file.

To run tests simply run the `pytest` command within the Jeeves directory.

## Notes
Jeeves was designed for use by Red Hat OpenStack QE and the organization's production CI environment - while the project can be used for other Jenkins environments, it may require some tweaking to work as expected.
