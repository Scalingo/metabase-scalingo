# Deploy metabase on Scalingo

## Steps to deploy metabase

1. Create an application on Scalingo

```
scalingo create my-metabase
```

2. Add a PostgreSQL for the internal usage of Metabase

```
scalingo -a my-metabase addons-add postgresql postgresql-starter-512
```

3. Configure multi-buildpack in the app environment

```
scalingo -a my metabase env-set 'BUILDPACK_URL=https://github.com/Scalingo/multi-buildpack'
```

4. Clone this repository

```
git clone https://github.com/Scalingo/metabase-scalingo
```

5. Configure GIT

```
cd metabase-scalingo
scalingo -a my-metabase git-setup
```

6. Deploy the application

```
git push scalingo master
```
