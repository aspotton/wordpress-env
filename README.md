# WordPress Docker Environment

A quick way to run `docker-compose up` and have an environment with WordPress and MySQL database. The primary use case is for development work. The PHP version in the WordPress image is 7.2.x.

You can clone this repository and use it to store your WordPress content files during development inside the `wp-content` directory. The installation files are provided by the `wordpress` image but you can keep track of themes and plugins here.

*** NOTE *** There are no themes or plugins installed when first run. You will need to install at a theme after the initial run to be useful.

## Usage

```
docker-compose up
```

For customizations options, see below.

## Data Persistence

 * WordPress
   * The installation files are provided by the base image using the version you specified when calling `docker-compose up`. These aren't saved to the local directory.
   * Save any themes or plugins in the `wp-content` directory. These are synced locally.
 * Database
   * Data is saved inside the `wordpress_db_data` docker volume

### Database Backup

```
docker exec wordpress_db_1 mysqldump -u root -psomewordpress wordpress > database.sql
```

## Customizations

If you migrate from lower to higher MySQL version the DB engine *should* be able to migrate your data successfully. If not, consider backing up your data, removing the docker volume `wordpress_db_data`, and re-importing the data into the new version.

### WordPress Version
By default the latest official version of WordPress is used. If you need an environment with a specific version you can pass in the environment variable `WORDPRESS_VERSION`. For example, using WordPress 4.8:

```
WORDPRESS_VERSION=4.8 docker-compose up
```

### MySQL Version
By default MySQL 5.7 is used. If you need an environment with a specific version you can pass in the environment variable `MYSQL_VERSION`. For example, MySQL 5.6:

```
MYSQL_VERSION=5.6 docker-compose up
```
