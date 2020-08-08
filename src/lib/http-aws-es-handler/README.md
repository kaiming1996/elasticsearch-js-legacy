# Connection External Kibana with Amazon Elasticsearch
Makes [elasticsearch-js](https://github.com/elastic/elasticsearch-js) compatible with Kibana. It uses the aws-sdk to make signed requests to an Amazon ES endpoint.

## Installation
```bash
npm install --save aws-sdk 
```
Change the orginial Elasticsearch dependency inside package.json to the directory of modified Elasticsearch.

Inside the Kibana folder: 
Run yarn kbn bootstrap
Run yarn kbn start --oss 

## Usage

Make sure the AWS credentials/regions/endpoints are in the enviorment variable. 

Or we can change the configuration inside the src/lib/client.js file 



```javascript
AWS.config.update({
      credentials: new AWS.EnvironmentCredentials('AWS'), //or build your credentials here
      region: process.env.AMAZON_ELASTICSEARCH_REGION || 'us-west-2' //or type your region here
      });

    if (!config.hosts && !config.host) {
      config.host = process.env.AMAZON_ELASTICSEARCH_DOMAIN || 'localhost:9200'; //or type your endpoint here
    }
```

