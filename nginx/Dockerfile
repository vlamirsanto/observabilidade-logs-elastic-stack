FROM nginx:latest

RUN rm -f /var/log/nginx/access.log && rm -f /var/log/nginx/error.log

# Id do usuário
ARG ELASTIC_VERSION=7.11.2

# Log instrumentation
RUN curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-${ELASTIC_VERSION}-amd64.deb \
    && dpkg -i filebeat-${ELASTIC_VERSION}-amd64.deb
COPY ./nginx/filebeat.yml /etc/filebeat

# Metric instrumentation
RUN curl -L -O https://artifacts.elastic.co/downloads/beats/metricbeat/metricbeat-${ELASTIC_VERSION}-amd64.deb \
    && dpkg -i metricbeat-${ELASTIC_VERSION}-amd64.deb
COPY ./nginx/metricbeat.yml /etc/metricbeat

COPY ./nginx/entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]