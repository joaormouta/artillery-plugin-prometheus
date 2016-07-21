# artillery-plugin-influxdb
Plugin for Artillery.IO that records response data into InfluxDB.

To use:

1. `npm install -g artillery`
2. `npm install artillery-plugin-influxdb`
3. Add `influxdb` Plugin config to your "`hello.json`" Artillery script

    ```json
    {
      "config": {
        "plugins": {
            "influxdb": {
                "testName": "my_load_test_case",
                "measurementName": "Latency",
                "testRunId": "342-233-221",
                "tags": {
                    "environment": "joes-dev-box",
                    "host": "joe-dev.somewhere.org"
                },
                "influx": {
                    "host": "my.influx.server.com",
                    "username": "joe_developer",
                    "password": "1t`sA$3cr3t",
                    "database": "load_test_results"
                }
            }
        }
      }
    }
    ```

4. `artillery run hello.json`

This will cause every latency to be published to the given InfluxDB instance.

If no `testRunId` property is provided, a UUID is generated for the run.

The `measurementName` config property is optional, 'latency' will be used by default.

The `tags` property is also optional. The `testRunId` and `testName` are always written as tags with any sample reported.

## Using environment variables to store credentials

The environment variables `INFLUX_USERNAME` and `INFLUX_PASSWORD` may be set instead of
passing 'username' and/or 'password' properties in the config file.

For more information, see:

* https://github.com/shoreditch-ops/artillery
* https://github.com/node-influx/node-influx

Enjoy!
