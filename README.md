# Rails database yml

Generates a `config/database.yml` file with the environment information from your database service.

For this step you need to have a mysql or postgres. See the [services](http://devcenter.wercker.com/articles/services/) on wercker devcenter for more information about services.

# What's new

- Add `postgresql-min-message` parameter

# Options

- `service` This option is not required. If set, it will load the template from the specified service; otherwise, it will infer the service from the environment.
- `postgresql-min-message` (optinal, default: `warning`): Set the min_messages parameter in the postgresql template.

# Example

The following `wercker.yml`:

``` yaml
box: wercker/ruby
services:
  - wercker/postgresql
build:
  steps:
    - rails-database-yml
```

Will generate the following `config/database.yml`:

``` yaml
test:
    adapter: postgresql
    encoding: "utf8"
    database: <%= ENV['WERCKER_POSTGRESQL_DATABASE'] %><%= ENV['TEST_ENV_NUMBER'] %>
    username: <%= ENV['WERCKER_POSTGRESQL_USERNAME'] %>
    password: <%= ENV['WERCKER_POSTGRESQL_PASSWORD'] %>
    host: <%= ENV['WERCKER_POSTGRESQL_HOST'] %>
    port: <%= ENV['WERCKER_POSTGRESQL_PORT'] %>
    min_messages: warning
```

# Changelog

## 1.0.0

- Add `postgresql-min-message` parameter

## 0.9.3

- Use `$PWD` instead of `$WERCKER_ROOT_DIR`

## 0.9.2

- Adds environment variable `TEST_ENV_NUMBER` to the database name

## 0.9.1

- Initial version
