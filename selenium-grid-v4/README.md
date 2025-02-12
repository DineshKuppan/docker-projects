## Setting up Selenium Grid 4 with Docker Compose
Selenium Grid is a powerful tool for running multiple tests on different browsers, operating systems, and machines in parallel. It allows you to run tests in parallel, which can significantly reduce the time it takes to run your test suite. In this article, we will show you how to set up Selenium Grid 4 with Docker Compose.

### To Set up Selenium Grid 4 (Hub) with Docker Compose, you need to follow the below steps:

1. Browser Node 1 - Google Chrome
2. Browser Node 2 - Mozilla Firefox

```bash
docker-compose up -d
```
(or)
```bash
docker-compose -f docker-compose.yml up -d
```

### To Set Up Selenium Grid 4 (Node) with Docker Compose, you need to follow the below steps:

```bash
docker-compose -f docker-compose-node-1.yml up -d
```

### Here is my Network Configuration (Home)

#### WiFi Default IP Address

The default IP address in most of our home Wi-Fi network is `192.168.1.1`.

Devices Connected to my Wi-Fi Network

The following devices are connected to the network:

|    Device Name    |    IP Address      |   Description   |
|-------------------|--------------------|-----------------|
|    Device 1       |    192.168.1.2     |    Selenium Grid Hub & Node 1 - Chrome (Runs)  |
|    Device 2       |    192.168.1.3     |    Selenium Grid Node 2 (Runs) - Firefox       |

The most important thing to note is that the IP address of the device running the Selenium Grid Hub has to configured properly in Selenium Node 2

Inside the `docker-compose-node-1.yml` file, you need to set the following environment variables:

1. Selenium Grid Hub IP Address: `192.168.1.2`
2. Selenium Grid Hub Port: `4444`
3. Selenium Grid Node 1 IP Address: `192.168.1.3`
4. Selenium Node 1 Port - `5555`

```bash
- SE_EVENT_BUS_HOST=192.168.1.2
- SE_EVENT_BUS_PUBLISH_PORT=4442
- SE_EVENT_BUS_SUBSCRIBE_PORT=4443
- SE_NODE_GRID_URL=http://192.168.1.3:5555
- SE_NODE_HOST=192.168.1.3
```

### Additional information:

*SE_NODE_MAX_INSTANCES:* This defines how many instances of same version of browser can run over the Remote System.
*SE_NODE_MAX_SESSIONS:* This defines maximum number of concurrent sessions that will be allowed.
