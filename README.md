# Rails database yml

Generates a `config/database.yml` file with the environment information from your database service.

For this step you need to have a mysql or postgres. See the [services](http://devcenter.wercker.com/articles/services/) on wercker devcenter for more information about services.

## Example

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
  encoding: sql_ascii
  database: <%= ENV['WERCKER_POSTGRESQL_DATABASE'] %>
  username: <%= ENV['WERCKER_POSTGRESQL_USERNAME'] %>
  password: <%= ENV['WERCKER_POSTGRESQL_PASSWORD'] %>
  host: <%= ENV['WERCKER_POSTGRESQL_HOST'] %>
  port: <%= ENV['WERCKER_POSTGRESQL_PORT'] %>
```
