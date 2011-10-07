============
Installation
============

Pre-requisites
==============

Ubuntu (10+ /  Lucid or Higher)
--------------------------------

Install the following::

    sudo apt-get install python-setuptools python-dev libpq-dev
    sudo easy_install pip
    sudo pip install virtualenv

Main instructions
=================

These instructions install OpenComparison on your computer, using PostgreSQL and sample data.

Git clone the project and install requirements
------------------------------------------------

Create a virtualenv, activate it, git clone the OpenComparison project, and install its requirements::

    cd <installation-directory>
    virtualenv env-oc
    source env-oc/bin/activate
    git clone git@github.com:opencomparison/opencomparison.git opencomparison
    cd opencomparison
    pip install -r requirements/mkii.txt

Set up local settings
---------------------

In the ``settings/`` directory, Copy the ``local_settings.py.example`` to ``local_settings.py``::

    cd settings
    cp local_settings.py.example local_settings.py

Change the ``ROOT_URLS`` setting in ``local_settings.py`` from `<root_directory_name>` to the correct value (i.e. the name of your repo)::

    ROOT_URLCONF = '<root_directory_name>.urls'

OPTIONAL! You can enable launchpad support in the local settings file. Launchpad's dependencies can be a little fussy, so this will probably require some additional tweaking on your part::

    LAUNCHPAD_ACTIVE = False

Add a Google Analytics code if you have one::

    URCHIN_ID = "UA-YOURID123-1"

Setup your email settings::

    DEFAULT_FROM_EMAIL = 'Your Name <me@mydomain.com>'
    EMAIL_SUBJECT_PREFIX = '[Your Site Name] '

Change the ``SECRET_KEY`` setting in ```local_settings.py``` to your own secret key::

    SECRET_KEY = "CHANGE-THIS-KEY-TO-SOMETHING-ELSE"

Set up your PostgreSQL database
-------------------------------

Set up PostgreSQL and create a database as per the postgresql_ contributor instructions.

Make your database::

    python manage.py syncdb
    python manage.py migrate

Then, load the flatpages fixtures::

    python manage.py loaddata fixtures/flatpages.json

OPTIONAL! Load some base data for development usage. This should not be loaded on the production site::

    python manage.py loaddata

Load the site in your browser
-----------------------------

Run the development server::

    python manage.py runserver

Then point your browser to http://127.0.0.1:8000

Give yourself an admin account on the site
------------------------------------------

Create a Django superuser for yourself, replacing joe with your username/email::

    python manage.py createsuperuser --username=joe --email=joe@example.com


.. _postgresql: postgresql_contributor_instructions.html
.. _faq: faq
