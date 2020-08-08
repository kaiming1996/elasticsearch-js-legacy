# AWS/Kibana Compatible Elasticsearch.js Modified Version 7.4

---

#### Install this Elasticsearch js client to connect locally configured external Kibana(7.4) with Amazon Elasticsearch Endpoint(7.4)

Modify the [elasticsearch-js](https://github.com/elastic/elasticsearch-js) to make it compatible with Kibana. It uses the [aws-sdk](https://aws.amazon.com/sdk-for-node-js/) to make signed requests to Amazon ES endpoints.

This is the solution for accessing your cluster from local [Kibana](https://github.com/elastic/kibana/tree/7.4) of version 7.4 and earlier 

## Installation

Download the [modified version](https://github.com/kaiming1996/elasticsearch-js-legacy)
```bash
git clone https://github.com/kaiming1996/elasticsearch-js-legacy.git 
```
Set AWS credentials inside the environment
 ```bash                     
export AWS_ACCESS_KEY_ID=XXXXXXXXXXXXXXXXXXX
export AWS_SECRET_ACCESS_KEY=XXXXXXXXXXXXXXXXXXX
export ELASTICSEARCH_REGION=XXXXXXXXXXXXXXXXXXX
export ELASTICSEARCH_DOMAIN=XXXXXXXXXXXXXXXXXXX
```

Inside your own Kibana package.json, change the orginial Elasticsearch dependency from "elasticsearch": "^16.4.0", to "elasticsearch": "path_to_modified_es_js_client"

![dependency](https://github.com/kaiming1996/elasticsearch-js-legacy/blob/kaiming1996-kibana-es-handler/screenshot/dependency.png)

## Usage

Original install method (e.g. download page, yum, from source, etc.): Kibana from GitHub

Steps to reproduce:

1. Download the [modified version](https://github.com/kaiming1996/elasticsearch-js-legacy)
2. Set AWS credentials
3. Change the orginial Elasticsearch dependency inside package.json inside the Kibana from Github
4. Reinstall the dependency in the Kibana directory
 ```bash                     
 yarn kbn bootstrap
 ``` 
5. Run the Kibana in the Kibana directory with "--oss"
 ```bash                     
 yarn start --oss
 ``` 


If the environment variables are not working, we can directly change the configuration inside the [client.js](https://github.com/kaiming1996/elasticsearch-js-legacy/blob/kaiming1996-kibana-es-handler/src/lib/client.js) file 
```javascript
AWS.config.update({
      credentials: new AWS.EnvironmentCredentials('AWS'), //or build your credentials here
      region: process.env.ELASTICSEARCH_REGION || 'us-west-2' //or type your region here
      });

    if (!config.hosts && !config.host) {
      config.host = process.env.ELASTICSEARCH_DOMAIN || 'localhost:9200'; //or type your endpoint here
    }
```

You should be able to view your visualized data at http://localhost:5603
![result](https://github.com/kaiming1996/elasticsearch-js-legacy/blob/kaiming1996-kibana-es-handler/screenshot/result.png)


## Features
 It has all the original features from the elasticsearch js client, including: 
 
 - One-to-one mapping with REST API and the other official clients
 - Generalized, pluggable architecture. See [Extending Core Components](https://www.elastic.co/guide/en/elasticsearch/client/javascript-api/16.x/extending_core_components.html)
 - Configurable, automatic discovery of cluster nodes
 - Persistent, Keep-Alive connections
 - Load balancing (with pluggable selection strategy) across all available nodes.


## Credits

Adopted from this [gist](https://github.com/TheDeveloper/http-aws-es/blob/master/connector.js). Thanks [@TheDeveloper](https://github.com/TheDeveloper)
