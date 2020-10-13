# Scalyr Logstash Plugin

This is extended version from [ELK on Docker](https://github.com/deviantony/docker-elk) with Filebeat and Scalyr plugins. Filebeat will log nginx access logs. Send them through Filebeat to Logstash which sends the body to scalyr.

This is to be used as a template to templatize the use of the scalyr logstash plugin. 

## What's inside

```
├── app
│   ├── package.json
│   ├── package-lock.json
│   ├── src
│   │   └── index.js
│   └── yarn.lock
├── elasticsearch
│   ├── config
│   │   └── elasticsearch.yml
│   └── Dockerfile
├── filebeat
│   ├── config
│   │   └── filebeat.yml
│   └── Dockerfile
├── kibana
│   ├── config
│   │   └── kibana.yml
│   └── Dockerfile
├── logstash
│   ├── config
│   │   └── logstash.yml
│   ├── Dockerfile -- install scalyr
│   └── pipeline
│       └── nginx.conf
├── nginx
│   ├── config
│   │   └── site.conf
│   ├── Dockerfile
│   └── log
│       ├── access.log
│       └── error.log
├── docker-compose.yml
├── LICENSE
└── README.md
```

- App: minimal simple Express app
- Nginx: web server for app.
- Elasticsearch: containing build image and configure for Elasticsearch
- Filebeat: containing build image and configure for Filebeat to streaming log of Nginx to Logstash
- Logstash: containing build image and configure pipeline for Logstash to process sent log file from Filebeat. Then downloads the scalyr plugin. 
- Scalyr Plugin: is installed with the logstash build. Just provide an api key 
- Kibana: containing build image and configure for Kibana to visualize data

## Getting Started
First set the scalyr api key this is located in `./logstash/pipeline/nginx.conf`

Troubleshooting tip: you may need to grant permissions for your local machine to share the `/nginx/log/*.log` files

To run this stack, run the following command
```bash
docker-compose up
```
Enter an api key to your scalyr instance and view your app and access logs in scalyr. 

Default Kibana user information
- Username: elastic
- Password: changeme
