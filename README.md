# snap publisher plugin - Graphite

This plugin publishes metrics to graphite.

1. [Getting Started](#getting-started)
  * [System Requirements](#system-requirements)
  * [Installation](#installation)
  * [Configuration and Usage](configuration-and-usage)
2. [Documentation](#documentation)
  * [Examples](#examples)
  * [Roadmap](#roadmap)
3. [Community Support](#community-support)
4. [Contributing](#contributing)
5. [License](#license)
6. [Acknowledgements](#acknowledgements)

### System Requirements
* Snap Daemon running

### Installation
#### Download Graphite plugin binary:
You can get the pre-built binaries for your OS and architecture at snap's [Github Releases](https://github.com/intelsdi-x/snap-plugin-publisher-graphite/releases) page.

#### To build the plugin binary:
Fork https://github.com/intelsdi-x/snap-plugin-publisher-graphite
Clone repo into `$GOPATH/src/github/intelsdi-x/`:  
```
$ git clone https://github.com/<yourGithubID>/snap-plugin-publisher-graphite
```
Build the plugin by running make in repo:
```
$ make
```
This builds the plugin in `/build/$GOOS/$GOARCH`

### Configuration and Usage
* Set up the [Snap framework](https://github.com/intelsdi-x/snap/blob/master/README.md#getting-started)

## Documentation
[graphite](https://graphite.readthedocs.org/en/latest/)

### Examples


#### Example task
Example task manifest to use Graphite plugin:
```json
{
    "version": 1,
    "schedule": {
        "type": "simple",
        "interval": "1s"
    },
    "workflow": {
        "collect": {
            "metrics": {
                "/intel/mock/foo": {},
                "/intel/mock/bar": {},
                "/intel/mock/*/baz": {}
            },
            "config": {
                "/intel/mock": {
                    "user": "root",
                    "password": "secret"
                }
            },
            "process": [
                {
                    "plugin_name": "passthru",
                    "publish": [
                        {
                            "plugin_name": "graphite",
                            "config": {
                                "server": "127.0.0.1",
                                "port": 2003
                            }
                        }
                    ]
                }
            ]
        }
    }
}
```

List of config arguments:
* "server" (required) - the IP of graphite host.
* "port" (optional) - 2003 by default.
* "prefix_tags" (optional) - coma separated list of metric tags used to add prefix on the published name, "plugin_running_on" by default.
* "prefix" (optional) - change the published name prefix, happens before prefixes from "prefix_tags".

### Roadmap
There isn't a current roadmap for this plugin, but it is in active development. As we launch this plugin, we do not have any outstanding requirements for the next release.

If you have a feature request, please add it as an [issue](https://github.com/intelsdi-x/snap-plugin-publisher-graphite/issues/new) and/or submit a [pull request](https://github.com/intelsdi-x/snap-plugin-publisher-graphite/pulls).

## Community Support
This repository is one of **many** plugins in **snap**, a powerful telemetry framework. See the full project at http://github.com/intelsdi-x/snap To reach out to other users, head to the [main framework](https://github.com/intelsdi-x/snap#community-support)

## Contributing
We love contributions!

There's more than one way to give back, from examples to blogs to code updates. See our recommended process in [CONTRIBUTING.md](CONTRIBUTING.md).

## License
[snap](http://github.com:intelsdi-x/snap), along with this plugin, is an Open Source software released under the Apache 2.0 [License](LICENSE).

## Acknowledgements
List authors, co-authors and anyone you'd like to mention

* Author: [Cody Roseborough](https://github.com/ircody)

And **thank you!** Your contribution, through code and participation, is incredibly important to us.
