#FROM apache/airflow:2.3.3-python3.8 as build
FROM apache/airflow:2.3.3-python3.8 as build
ENV ACCEPT_EULA=Y
# Attach Labels to the image to help identify the image in the future
LABEL maintainer="atk"

USER root

RUN apt-get remove -y msodbcsql18 && \
    apt-get autoremove -yqq --purge && apt-get clean && \
    apt-get update && apt-get -y upgrade && \
    apt-get -y install default-libmysqlclient-dev  gcc  python3.8-dev && \
    apt-get install -y  msodbcsql18  && \
    pip3 install mysqlclient

COPY --chown=airflow:root dags /opt/airflow/dags

USER airflow

# Airflow user in Docker image version 2.2.0+ moved to root group to be compatible with Open-Shift (https://airflow.apache.org/docs/docker-stack/entrypoint.html#allowing-arbitrary-user-to-run-the-container),
# below COPY is from official example: https://airflow.apache.org/docs/docker-stack/build.html#example-when-you-want-to-embed-dags
