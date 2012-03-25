## Dbmanager

This gem will add some convenience rake tasks that will help you manage db dumps
and imports.

### Database Imports

rake db:import

You will be prompted to choose the source and the target environment db, and the
source db will be imported into the target db. Production db is protected, which
means you cannot overwrite it unless you explicitly override this setting in the
override file (see "override database.yml")

### Database Dumps

rake db:dump

You will be prompted to choose the target dir (defaults to tmp) and the sql file
name (sql extension will be added automatically). If the file already exists, it
will be overwritten.

### Override database.yml

Since some settings may be specific to the server environment (ie. host could
be a private ip not reachable from anywhere) you can overwrite the settings in
database.yml by adding a dbmanager_override.yml file in your rails config dir.
Another use is to set some environments as protected, or vice versa allow to
overwrite production env.
For example if we want to override the following setting, and make the database
protected from overwriting:

beta:
  host: 123.123.123.123

we should put in dbmanager_override.yml this:

beta:
  host: 234.234.234.234
  protected: true

Instead, if we want to make production writable we should add this:

production:
  protected: false
