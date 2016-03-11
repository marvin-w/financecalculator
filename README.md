# FinanceCalculator

This file covers some documentation about the finance calculator as well as used software, how to install and things that need to be done to get the application up and running.

## Installation

Installation of this ruby on rails app is really straight forward.

* Adjust the file `config/database.yml` to fit your needs.
* Simply run the following command:

    bin/rake db:migrate RAILS_ENV=production
    bin/rake assets:precompile


### Dependencies

One dependency you need to worry about right now is Ruby in Version ´>=2.1.4´.

### Webserver

Every major webserver with proper ruby support is great to be used with this rails application. Moreover I'd recommend to use "shit i dont remember" to run the application
and then use a reverse proxy like nginx to set up your webserver.

## Planning

### Features

* I can track my finances.
* Finances are defined as income and outcome.
* Finances can be recurring on a specific period of time.
* I can add new finances in the web interface.
* A dashboard should show historical data of finances.
* Optionally: Email notifications when a new periodic element is added to the existing finances.
* Finances that I add are associated with a user.
* There should be a view to differentiate between the current time and the end of a time unit (months probably)

Therefor the following user specific features need to be existent:

* There must be a way to reset a password of a user
* It should be possible to register a new user in the webinterface
* It should not be possible to track finances if you aren't logged in
* It should be possible to log in as a registrated user.

### Models

The following models are needed to obtain the required features.

####  Finance Model

Takes care of all finances in the application.

Columns:
* id unsinged int PK AI
* finance_type uint FK FinanceType.type
* recurring_id uint FK RecurringFinance.id DEFAULT NULL
* amount float check>0 enforce amounts to be positive always.
* name varchar
* description varchar
* created_at TIME
* updated_at TIME

#### FinanceType Model

Defines the different types of finances exist in the whole application.

Default: Income, Outcome

Columns:
* type varchar
* description varchar

#### RecurringFinance Model

Takes care of recurring finances in the application.

Columns:
* id
* minute
* hour
* weekday
* month
* year
* times