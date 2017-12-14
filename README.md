Testing ImageJ Updater
======================

[ijtest/docker-compose.yml](ijtest/docker-compose.yml) provides
a sandbox for testing ImageJ Updater behavior. This is done by
using an internal network, which permits no connections to outside
resources. Only inner container connections are possible.

The mirrored update sites created under "Setup" below are then
linked into the Docker containers with the expected alias. If
`./ImageJ-linux64 --update ...` tries to access any other URL,
there will be a short hang before a stacktrace is printed.

An ownCloud WebDav server is also started in case the client
would like to push to a clean update site.

Setup
-----

* install docker, docker-compose, etc.
* `wget --mirror update.imagej.net # 1GB`
* `wget --mirror update.fiji.sc # 2.4GB`
* Make any necessary changes to the mirrored directories.
  This does not *yet* support using the provided NGINX
  instances for uploading, though that is likely doable
  as well.

Usage
-----

 * `cd ijtest`

 * Execute: `docker-compose up --abort-on-container-exit`
   and watch the output (See [example_out.txt](example_out.txt))

 * Make changes to the `command:` element for the client
   container to see different behavior *or* change the command
   to `bash` for interacting with the container. Use:
   `docker-compose exec client bash` to enter the started
   container.
