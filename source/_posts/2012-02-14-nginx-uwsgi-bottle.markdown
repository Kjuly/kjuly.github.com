---
layout: post
title: "NginX + uWSGI + Bottle"
date: 2012-02-14 15:19
comments: true
categories: 
- Web
- NginX
- Python
---

### Nginx

Prerequisites:

- PCRE(Perl Compatible Regular Expressions)
- OpenSSL:

        ./Configure darwin64-x86_64-cc
        make
        make install

Intall Nginx:

    ./configure --with-cpu-opt="amd64" --with-http_ssl_module
    make
    sudo make install

Testing Nginx by runing Nginx:

    cd /usr/local/nginx/sbin
    sudo ./nginx

Visit [http://127.0.0.1/](http://127.0.0.1/) and will show `"Welcome to nginx!"`.

Stop it:

    sudo ./nginx -s stop

Reload the configuration:

    sudo ./nginx -s reload

Nginx's config file path ([Nginx Configuration Primer][]):

    /usr/local/nginx/conf/nginx.conf


---
### uWSGI:

    sudo pip install uwsgi


Test `uWSGI` with a simple WSGI app:  
`path/to/project/hello.py`:

{% codeblock lang:python %}
def application(env, start_response):
    start_response('200 OK', [('Content-Type','text/html')])
    return "Hello World"
{% endcodeblock %}

Then run:

    uwsgi --http :9090 --wsgi-file path/to/project/hello.py

Visit [http://localhost:9090](http://localhost:9090).


---
### Bottle + uWSGI + Nginx:

Modify `/usr/local/nginx/conf/nginx.conf`:

{% codeblock lang:c %}
...
location / {
    include uwsgi_params;
    uwsgi_pass 127.0.0.1:3031;
}
...
{% endcodeblock %}

`path/to/project/app.py`:

{% codeblock lang:python %}
import os
from bottle import route, run, default_app

@route('/')
def main():
    return "Hello World~~~~~"

if __name__ == "__main__":
    # Interactive mode
    run(host='localhost', port=8080)
else:
    # Mod WSGI launch
    os.chdir(os.path.dirname(__file__))
    application = default_app()
{% endcodeblock %}

Run `Nginx` & `uWSGI`:

    sudo /usr/local/nginx/sbin/nginx
    uwsgi --http :3031 --wsgi-file path/to/project/app.py
    # or 
    # cd path/to/project
    # uwsgi --http :3031 --wsgi-file ./app.py
    #

or create a |config.yaml|(there're other type of files) file with settings, and run:

    uwsgi --yaml config.yaml

`config.yaml`:

{% codeblock lang:c %}
uwsgi:
  wsgi-file: /path/to/project/app.py  # or simple ./app.py
  http: 127.0.0.1:3031
{% endcodeblock %}
Configuration options can be refered at [uWSGI Documentation][]

Stop `uWSGI` & `Nginx`:

    # Maybe will use "uwsgi --stop uwsgi-app.pid", but just `^ C` is okay.
    sudo /usr/local/nginx/sbin/nginx -s stop

`uwsgi-app.pid` stores the thread ID like `1234`, `--stop`/`--reload` will "sends a SIGINT/SIGHUP to the pid written in `<pidfile>`".

---
### virtualenv

---
## References:

- [Nginx Official Install][]
- [Other Tips on Installing Nginx][]
- [uWSGI Installation (from sources)][]
- [Nginx Configuration Primer][]
- [uWSGI Quickstart][]
- [uWSGI Example][]
- [uWSGI Documentation][]

[NginX Official Install]: http://wiki.nginx.org/Install
[Other Tips on Installing NginX]: http://wiki.nginx.org/Installing_on_Solaris_10_u5
[uWSGI Installation (from sources)]: http://projects.unbit.it/uwsgi/wiki/Install
[Nginx Configuration Primer]: http://blog.martinfjordvald.com/2010/07/nginx-primer/
[uWSGI Quickstart]: http://projects.unbit.it/uwsgi/wiki/Quickstart
[uWSGI Example]: http://projects.unbit.it/uwsgi/wiki/Example
[uWSGI Documentation]: http://projects.unbit.it/uwsgi/wiki/Doc
