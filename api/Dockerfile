FROM irekua-main

# Install apache
RUN apt-get install -y apache2 apache2-utils apache2-dev

# Install mod_wsgi
# Download and extract
RUN curl -L -o mod_wsgi.tar.gz https://github.com/GrahamDumpleton/mod_wsgi/archive/4.6.5.tar.gz
RUN mkdir mod_wsgi
RUN tar xvzf mod_wsgi.tar.gz -C mod_wsgi --strip-components=1
RUN rm mod_wsgi.tar.gz

# Configure compile and install
RUN cd mod_wsgi && \
    /bin/bash -c "./configure --with-python=/venv/bin/python" && \
    make && \
    make install

# Clean
RUN cd ..
RUN rm -r mod_wsgi

# Add app to web directory
RUN cp -r irekua/irekua /var/www/irekua
RUN rm -r irekua

# Configure apache
ADD irekua_site.conf /etc/apache2/sites-available/000-default.conf

# Expose database port
EXPOSE 5432

# Add database configuration arguments
ENV DB_USER="irekua"
ENV DB_HOST="localhost"
ENV DB_PASSWORD="password"
ENV DB_NAME="irekua"

# Add static and media url config
ENV STATIC_URL="http://localhost/"
ENV STATIC_ROOT="/static/"
ENV MEDIA_URL="http://localhost/"
ENV MEDIA_ROOT="/media/"

CMD apachectl -D FOREGROUND
