# Eikon-docker

Use Refinitiv's Python Eikon Data API within a Docker container. The host of this package has to have the Eikon desktop installed.

If you don't 
## Installation
```python
pip install eikon-docker
```

## Hints

I am using Make throughout all my projects. It's not a native Windows tool. You can however make it work following

https://gist.github.com/evanwill/0207876c3243bbb6863e65ec5dc3f058

## Usage

I assume you are familiar with docker. If not, this package has no additional benefit for you. I recommend to use

https://pypi.org/project/eikon/

However, if you share my love for docker you may prefer having a somewhat cleaner setup and package all tools neatly in one
container. I have not changed the API etc.

All the Eikon commands you are familiar will continue to work (or continue to be broken). The difference is now that the Eikon code
lives together with its dependencies in a container. Here's a little fragment:

```
import eikon as ek
print(ek.__version__)

import logging
import http.client

http.client.HTTPConnection.debuglevel = 1

logging.basicConfig()
logging.getLogger().setLevel(logging.DEBUG)
requests_log = logging.getLogger("requests.packages.urllib3")
requests_log.setLevel(logging.DEBUG)
requests_log.propagate = True

if __name__ == '__main__':
    ek.set_app_key('084dd01c11d749f884ba12d60c2673697ec0fa2e')

    df = ek.get_timeseries(["MSFT.O"],
                           start_date="2016-01-01",
                           end_date="2016-01-10")
    print(df)
```



## License

Refinitiv has released the Python Eikon Data API using the Apache 2.0 license. By design this package will only work if installed
within a container that is running on a host with an Eikon desktop installed. 