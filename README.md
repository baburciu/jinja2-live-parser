# Jinja2 live parser

A lightweight live parser for [Jinja2](http://jinja.pocoo.org/docs/dev/) based on [Flask](http://flask.pocoo.org/) and [Jquery](http://jquery.com/).  
All you need is Python and preferably [pip](https://pypi.python.org/pypi/pip). Can parse JSON and YAML inputs.

## Install

### Clone + pip

    $ git clone git@github.com:baburciu/jinja2-live-parser.git
    $ pip install -r requirements.txt
    $ python parser.py

### Dockerfile

Build it:

    docker build -t mydocker/j2parser .
    docker run -d -p 5000:5000 mydocker/j2parser

Or simply pull it from registry (without building):

    docker run -d -p 5000:5000 sahilsk/j2parser


## Usage

You are all set, go to `http://<HOST_IP>:5000/` and have fun. The [Jinja2 Ansible Filters](https://pypi.org/project/jinja2-ansible-filters/) offer the filters Ansible provides, that are not present in upstream Jinja2. :deciduous_tree:
You can add any custom filter you'd like in `filters.py`.  Just make sure the function's name starts with `filter_`.

```shell
root@vm1:~# git clone https://github.com/baburciu/jinja2-live-parser.git
Cloning into 'jinja2-live-parser'...
remote: Enumerating objects: 90, done.
remote: Total 90 (delta 0), reused 0 (delta 0), pack-reused 90
Unpacking objects: 100% (90/90), done.
root@vm1:~#
root@vm1:~# python3 -m venv envs/jinja
root@vm1:~# source envs/jinja/bin/activate
(jinja) root@vm1:~# cd jinja2-live-parser/
(jinja) root@vm1:~/jinja2-live-parser#
(jinja) root@vm1:~/jinja2-live-parser# pip install -r requirements.txt
:
Installing collected packages: MarkupSafe, Jinja2, Werkzeug, itsdangerous, Flask, PyYAML, ipython
Successfully installed Flask-0.10.1 Jinja2-2.7.1 MarkupSafe-0.18 PyYAML-3.11 Werkzeug-0.9.6 ipython-2.2.0 itsdangerous-0.24
(jinja) root@vm1:~/jinja2-live-parser# head config.py
# Builtin config values: http://flask.pocoo.org/docs/0.10/config/
import os

DEBUG = os.environ.get('DEBUG', False)
#HOST = os.environ.get('HOST', 'localhost')
HOST = "0.0.0.0"     # <== make the Flask app answer to request from any IP, not only localhost sources
PORT = int(os.environ.get('PORT', 5000))

LOGGING_FORMAT = '%(asctime)s - %(name)s - %(levelname)s - %(message)s'
LOGGING_LOCATION = 'jinja2-live-parser.log'
(jinja) root@vm1:~/jinja2-live-parser#
(jinja) root@vm1:~/jinja2-live-parser# tail -5 parser.py
    app.run(
        host=config.HOST,
        port=config.PORT,
        debug=config.DEBUG,
    )
(jinja) root@vm1:~/jinja2-live-parser#
(jinja) root@vm1:~/jinja2-live-parser# python parser.py
 * Running on http://0.0.0.0:5000/
172.18.211.228 - - [17/Jan/2022 09:43:13] "GET / HTTP/1.1" 200 -
172.18.211.228 - - [17/Jan/2022 09:43:13] "GET /static/js/jquery-1.11.1.min.js HTTP/1.1" 200 -
172.18.211.228 - - [17/Jan/2022 09:43:13] "GET /static/css/style.css HTTP/1.1" 200 -
172.18.211.228 - - [17/Jan/2022 09:43:13] "GET /static/css/bootstrap.min.css HTTP/1.1" 200 -
172.18.211.228 - - [17/Jan/2022 09:43:13] "GET /static/js/bootstrap.min.js HTTP/1.1" 200 -
172.18.211.228 - - [17/Jan/2022 09:43:13] "GET /static/js/convert.js HTTP/1.1" 200 -
172.18.211.228 - - [17/Jan/2022 09:43:13] "GET /favicon.ico HTTP/1.1" 404 -
```

## Preview

![preview](http://i.imgur.com/T65xjAf.png)

