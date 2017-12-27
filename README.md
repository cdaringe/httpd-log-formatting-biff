# problem

timestamp formatting does not work in httpd.

see: https://stackoverflow.com/posts/47997641

# demo

the only change to the httpd conf file is the addition of the custom log formats.

for example:

```conf
ErrorLogFormat "{\
\"level\": \"%l\",\
...
\"timestamp\":\"%{<some-strftime-format>}t\"\
}"
```

to run, simply use the command:

```sh
docker run \
  -v `pwd`/http.alpine.conf:/usr/local/apache2/conf/httpd.conf \
  -dit httpd:2.4.29-alpine
```

this will run and fail, [expectedly](https://github.com/docker-library/httpd/issues/9). you just need to observe the logs, specifically how the time formatting is not honored.
