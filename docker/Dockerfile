ENV LANG en_US.UTF-8
RUN locale-gen en_US en_US.UTF-8

FROM python:2.7
ENV PYTHONUNBUFFERED 1

# keep upstart quiet
RUN dpkg-divert --local --rename --add /sbin/initctl
RUN ln -sf /bin/true /sbin/initctl

# install and stop nginx and supervisor
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install nginx supervisor
RUN echo "daemon off;" >> /etc/nginx/nginx.conf
RUN service supervisor stop
RUN service nginx stop

# place nginx and gunicorn confs at their specific location
RUN rm -f /etc/nginx/sites-enabled/*
run ln -s ./nginx.conf /etc/nginx/sites-enabled/
run ln -s ./supervisor.conf /etc/supervisor/conf.d/

RUN pip install supervisor-stdout

RUN mkdir /code
WORKDIR /code
ADD requirements.txt /code/

#RUN pip install -r requirements.txt
# create a virtual environment and install all depsendecies from pypi
RUN virtualenv /opt/venv
ADD ./requirements.txt /opt/venv/requirements.txt
RUN /opt/venv/bin/pip install -r /opt/venv/requirements.txt



cmd ["supervisord", "-n"]

