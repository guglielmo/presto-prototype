# Getting Started with Presto at Openpolis

## Introduction

This repository contains the files used to launch a protptype of [Presto](https://prestodb.io),
that is able to connect to differnet instances of postgresql.

They will setup a Presto cluster with connectors to 2 a postgresql server, a mysql server and
a [jupyter](https://jupyter.org/) instance, in order to work with both instances within a Presto connection.

The database connections are defined in `catalog/postgres.properties` and `catalog/mysql.properties`.

The jupyter notebook is found in ``jupyter/op_prototype.ipynb`` directory. It inserts some data into postgres,
some into mysql, and performs a join between the two instances.
It also shows the graph explaining the query execution, which I think helps newcomers understand how it all works.

## Requirements

- Docker (you can use [Docker CE](https://docs.docker.com/install/))
- Docker [Compose](https://docs.docker.com/compose/install/)

The prototype was developed on OS X, 
out the https://github.com/prestodb/f8-2019-demo project, by Greg Leclercq (Facebook) (thanks).

## Quick Start

To start the Presto cluster and its dependencies:
```
docker-compose up
```

Then open the Jupyter Notebook at [`localhost:8888`](http://localhost:8888).

The Jupyter Notebook password is `demo`. You can override it by changing the
SHA1 hash of `--NotebookApp.password='sha1:2017f6d8a65d:4f2115202d4cd8c081f1c135bc2b41292bcb4ec4'`
in `docker-compose.yml`.

The Presto UI is available at [`localhost:8080`](http://localhost:8080).

To run the Presto CLI:
```
docker-compose exec presto bin/presto-cli
```

You can find Presto's documentation on [prestodb.io/docs/current/](http://prestodb.github.io/docs/current/).

If you update a `Dockerfile`, use `docker-compose up --build` to ignore cache
and rebuild the images.

## Next Steps

In this prototype, all Presto nodes are run on the same machine. Presto has two types of nodes:
- The coordinator is the main server that compiles SQL And manages its execution
- The worker is a node that executes tasks scheduled by the coordinator

To run Presto in a distributed way, you will create a new instance with
`coordinator=false` in `etc/config.properties`.

- More about [deploying](http://prestodb.github.io/docs/current/installation/deployment.html) Presto
- Configuration properties [reference](http://prestodb.github.io/docs/current/admin/properties.html)
- [Developing](http://prestodb.github.io/docs/current/develop.html) extensions and integrations for Presto

## References

- https://prestodb.io
- https://github.com/prestodb/presto
- http://tinyurl.com/presto-paper
- https://prestodb.io/resources.html#libraries
- https://jupyter.org

## Contributing

Just fork and create a pull request, ad I'll see what can be done.

## License

presto-prototype is Apache 2.0 licensed, as found in the LICENSE file.
