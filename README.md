# SDH-Machine-Agora

Docker deployment of Agora and Curator.

This repository deploys these containers:
* RabbitMQ
* Curator
* Fountain
* Redis Database for Curator
* Redis Database for Fountain
* Planner
* Nginx

### Ports (container - host):
* RabbitMQ: 5672 - 5672
* RabbitMQ: 15672 - 15672
* Curator: 5007 - 5007
* Nginx: 80 - 9009

### Nginx Access:
|Nginx Path|Container/Path|
|:---------|:----------|
|/plan|planner/plan|
|/fragment|planner/fragment|
|/graph|fountain/graph|
|/types|fountain/types|
|/prefixes|fountain/prefixes|
|/properties|fountain/properties|
|/paths|fountain/paths|
|/seeds|fountain/seeds|
|/vocabs|fountain/vocabs|

### Docker - Requirements:

* docker > 1.7.0
* docker-compose > 1.3.1

### Docker - Usage:

|Alias|Command|
|:---------|:----------|
|Start|```docker-compose up -d```|
|Stop|```docker-compose stop```|
|Delete|```docker-compose rm -f```|
|Rebuild|```docker-compose build```|

### Docker - Tips:

If you want to change port redirection or configuration, we suggest you:

1. Stop
2. Delete
3. Build (if you have changed any file or physical configuration)
4. Start

### Agora - Usage:

After deployment, you must register seeds at Agora.

For that, you need to create HTTP (POST) Request for each seed.

Python code for register seeds easily:

* Replace 'seed_name' for your seed ontology
* Replace 'seed_url' for your seed url.

```
seed_name = 'org:ORGHarvester'
seed_url = 'http://.../orgharvester/'
```
```
import requests
import time

def seed(t, u):
    r = requests.post('http://...:9009/seeds', json={'type:t, 'uri':u})
    print 'Load {} seed: {}'.format(t, r.status_code)
    
c = False
co = 0
while not c:
    try:
        seed(seed_name, seed_url)
        c = True
    except Exception:
        co += 1
        if co > 5:
            break;
        time.sleep(1)
```




