docker-run-env
==============

Run docker run with all environment variables from the host exported to docker
run, and with the `--networking host` flag set. Useful for debugging docker
containers used in AWS lambda functions or batch jobs.

Use like:

```!sh
$ HELLO=world docker-run-env -- -it my_container python -c 'import os; print(os.environ["HELLO"])'
world
```

Works well with [swaj](https://github.com/f0rk/swaj) or [eruza](https://github.com/f0rk/eruza):
```!sh
$ swaj --profile dev exec docker-run-env -- -it my_container sh -c 'echo "$ENVIRONMENT"'
dev
```

Also good to chain with [lambda-env](https://github.com/f0rk/lambda-env) or [batch-env](https://github.com/f0rk/batch-env).
```!sh
$ swaj --profile dev exec lambda-env my_app docker-run-env -- -it my_container sh -c 'echo "$DB_URL"'
mysql://scott:tiger@localhost/dev
```

Supports an optional `--event` arg to export an environment variable EVENT with
the specified value from a file:
```!sh
$ docker-run-env --event /tmp/event.json -- -it my_container python -c 'import os; print(os.environ["EVENT"])'
{"hello": "world"}
```

Install
=======

```!sh
curl https://raw.githubusercontent.com/f0rk/batch-env/master/docker-run-env > ~/bin/docker-run-env
chmod +x ~/bin/docker-run-env
```
