FROM irekua-main

# Install nginx
RUN apt-get install -y nginx

# Generate static files
RUN /venv/bin/python irekua/irekua/manage.py collectstatic
RUN mkdir /var/www/irekua
RUN cp -r irekua/irekua/static/ /var/www/irekua/static/

# Clean directory
RUN rm -r irekua

ADD irekua_site /etc/nginx/sites-available/default

CMD ["nginx", "-g", "daemon off;"]
