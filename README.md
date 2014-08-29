# dokku-shoreman

dokku-shoreman is a plugin for [dokku][dokku] that injects a stripped down
version of [shoreman][shoreman], a Procfile runner written in bash.

Normally, dokku only runs the `web` process within Procfile. The dokku-shoreman
plugin will run all process types (web, worker, etc.) and stop them all together.

## This Fork

This fork changes the output style to be more verbose and log to STDOUT. This is
intended for [12 Factor Apps][12-factor] and can be collected with 
[logspout][logspout] and then [fluentd][fluentd].

Example output:

    2014-08-29T03:39:28+0000 web | 'bundle exec unicorn -N -p $PORT -c ./config/unicorn/production.rb' started with name web
    2014-08-29T03:39:30+0000 web | Refreshing Gem list
    2014-08-29T03:39:35+0000 web | listening on addr=0.0.0.0:5000 fd=10
    2014-08-29T03:39:35+0000 web | master process ready
    2014-08-29T03:39:35+0000 web | worker=0 ready
    2014-08-29T03:39:35+0000 web | worker=1 ready
    2014-08-29T03:39:35+0000 web | worker=2 ready
    2014-08-29T03:45:58+0000 web | method=GET path=/ format=html controller=api action=index status=200 duration=874.05 view=79.08 db=0.00

Also can be seen above is Rails [Lograge][lograge] formatting with one
line per request.

## Installation

```sh
git clone https://github.com/GeoCENS/dokku-shoreman.git /var/lib/dokku/plugins/dokku-shoreman
```

All future deployments will use shoreman to start all processes.

## License

The MIT License (MIT)

Copyright (c) 2013 Jason Staten

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

[dokku]: https://github.com/progrium/dokku
[shoreman]: http://hecticjeff.net/shoreman/
[12-factor]: http://12factor.net/logs
[logspout]: https://github.com/progrium/logspout
[fluentd]: http://www.fluentd.org/
[lograge]: https://github.com/roidrage/lograge
