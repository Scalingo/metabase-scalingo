![Metabase](metabase.png)

# Deploying Metabase to Scalingo

## Deploying using Scalingo's One-click button

Click on the button below to deploy Metabase to Scalingo within minutes.

[![Deploy](https://cdn.scalingo.com/deploy/button.svg)](https://my.scalingo.com/deploy?source=https://github.com/Scalingo/metabase-scalingo#master)

## Deploying using Scalingo's Command Line tool

1. Create an application on Scalingo:

```bash
$ scalingo create my-metabase
```

2. Add a PostgreSQL for the internal usage of Metabase:

```bash
$ scalingo --app my-metabase addons-add postgresql postgresql-starter-512
```

3. Configure your application to use the appropriate buildpack for deployments:

```bash
$ scalingo --app my-metabase env-set 'BUILDPACK_URL=https://github.com/Scalingo/multi-buildpack'
```

4. Clone this repository:

```bash
$ git clone https://github.com/Scalingo/metabase-scalingo
```

5. Configure `git`:

```bash
$ cd metabase-scalingo
$ scalingo --app my-metabase git-setup
```

6. Deploy the application:

```bash
$ git push scalingo master
```

# Configuring the application deployment environment

The following environment variables are available for you to adjust, depending
on your needs:

| Name                 | Description                                                                              | Default value                                       |
| -------------------- | ---------------------------------------------------------------------------------------- | --------------------------------------------------- |
| `BUILDPACK_URL`      | URL of the buildpack to use.                                                             | https://github.com/Scalingo/multi-buildpack.git[^1] |
| `DATABASE_URL`       | URL of your database addon. **Only available if you have a database addon provisioned**. | Provided by Scalingo                                |
| `MAX_METASPACE_SIZE` | Maximum amount of memory allocated to Java Metaspace[^2].                                | `512m` (512MB)                                      |

Metabase also supports many environment variables: [https://www.metabase.com/docs/latest/operations-guide/environment-variables.html](https://www.metabase.com/docs/latest/operations-guide/environment-variables.html).

[^1] [https://github.com/Scalingo/multi-buildpack.git](https://github.com/Scalingo/multi-buildpack.git)
[^2] See [https://wiki.openjdk.org/display/HotSpot/Metaspace](https://wiki.openjdk.org/display/HotSpot/Metaspace) for further details about Java Metaspace.

# Updating Metabase on Scalingo

To upgrade to the latest version of Metabase, you only need to redeploy it,
this will retrieve the latest version avaible on [the Metabase buildpack](https://github.com/metabase/metabase-buildpack).

## Updating after deploying using Scalingo's One-click button

If you deployed your Metabase instance via our One-click button, you can update
it with the following command:

```bash
$ scalingo --app my-metabase deploy https://github.com/Scalingo/metabase-scalingo/archive/refs/heads/master.tar.gz
```

## Updating after deploying using Scalingo's Command Line tool

```bash
$ cd metabase-scalingo
$ git pull origin master
$ git push scalingo master
```
