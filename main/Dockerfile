FROM python:3.6

LABEL version="1.0"
LABEL maintainer="smartinez@conabio.gob.mx"

# Install GDAL
RUN apt-get update
RUN apt-get install -y python3-dev
RUN apt-get install -y apt-utils
RUN apt-get install -y gdal-bin python3-gdal

# Set locales
RUN apt-get -y install locales
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
      locale-gen

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# Download irekua
RUN curl -o irekua.tar.gz -LJO https://github.com/CONABIO-audio/irekua/tarball/master
RUN mkdir irekua/
RUN tar -zxvf irekua.tar.gz -C irekua --strip-components=1
RUN rm irekua.tar.gz

# Create virtualenv
RUN pip install virtualenv
RUN virtualenv -p /usr/bin/python3 /venv

# Install all required packages
RUN /venv/bin/pip install -r irekua/requirements.txt
