![image](docs/source/images/VOLLTRON_Logo_Black_Horizontal_with_Tagline.png)

Distributed Control System Platform.

|Branch|Status|
|:---:|---|
|Master Branch| ![image](https://travis-ci.org/VOLTTRON/volttron.svg?branch=master)|
|3.x| ![image](https://travis-ci.org/VOLTTRON/volttron.svg?branch=3.x)|
|develop| ![image](https://travis-ci.org/VOLTTRON/volttron.svg?branch=develop)|

VOLTTRONTM is an open source platform for distributed sensing and control. The platform provides services for collecting and storing data from buildings and devices and provides an environment for developing applications which interact with that data.

## Features

* [Message Bus](http://volttron.readthedocs.io/en/master/core_services/messagebus/index.html#messagebus-index) allows agents to subcribe to data sources and publish results and messages
* [Driver framework](http://volttron.readthedocs.io/en/master/core_services/drivers/index.html#volttron-driver-framework) for collecting data from and sending control actions to buildings and devices
* [Historian framework](http://volttron.readthedocs.io/en/master/core_services/historians/index.html#historian-index) for storing data
* [Agent lifecycle managment](http://volttron.readthedocs.io/en/master/core_services/control/AgentManagement.html#agentmanagement) in the platform
* [Web UI](http://volttron.readthedocs.io/en/master/core_services/service_agents/central_management/VOLTTRON-Central.html#volttron-central) for managing deployed instances from a single central instance.

## Background

VOLTTRONTM is written in Python 2.7 and runs on Linux Operating Systems. For users unfamiliar with those technologies, the following resources are recommended:

https://docs.python.org/2.7/tutorial/
http://ryanstutorials.net/linuxtutorial/

## Installation

Install VOLTTRON by running the following commands which installs needed [prerequisites](http://volttron.readthedocs.io/en/master/devguides/setup/VOLTTRON-Prerequisites.html#volttron-prerequisites), clones the source code, then builds the virtual environment for using the platform.

```sh
sudo apt-get update
sudo apt-get install build-essential python-dev openssl libssl-dev libevent-dev git
git clone https://github.com/VOLTTRON/volttron
cd volttron
python bootstrap.py
```

This will build the platform and create a virtual Python environment. Activate this and then start the platform with:

```sh
. env/bin/activate
volttron -vv -l volttron.log&
```

This enters the virtual Python environment and then starts the platform in debug (vv) mode with a log file named volttron.log.

Next, start an example listener to see it publish and subscribe to the message bus:

```sh
scripts/core/make-listener
```

This script handles several different commands for installing and starting an agent after removing an old copy. This simple agent publishes a heartbeat message and listens to everything on the message bus. Look at the VOLTTRON log to see the activity:

```sh
tail volttron.log
```
Results in:

```sh
2016-10-17 18:17:52,245 (listeneragent-3.2 11367) listener.agent INFO: Peer: 'pubsub', Sender: 'listeneragent-3.2_1'
:, Bus: u'', Topic: 'heartbeat/ListenerAgent/f230df97-658e-45d3-8165-18a2ec834d3f', Headers:
{'Date': '2016-10-18T01:17:52.239724+00:00', 'max_compatible_version': u'', 'min_compatible_version': '3.0'},
Message: {'status': 'GOOD', 'last_updated': '2016-10-18T01:17:47.232972+00:00', 'context': 'hello'}
```

Stop the platform:

```sh
volttron-ctl shutdown --platform
```

## Next Steps
There are several [walkthroughs](http://volttron.readthedocs.io/en/master/devguides/index.html#devguides-index) to explore additional aspects of the platform:

* [Agent Development Walkthrough](http://volttron.readthedocs.io/en/master/devguides/agent_development/Agent-Development.html#agent-development)
* Demonstration of the [management UI](http://volttron.readthedocs.io/en/master/devguides/walkthroughs/VOLTTRON-Central-Demo.html#volttron-central-demo)

## Acquiring Third Party Agent Code
Third party agents are available under volttron-applications repository. In order to use those agents, add volttron-applications repository under the volttron/applications directory by using following command:

```sh
git subtree add –prefix applications https://github.com/VOLTTRON/volttron-applications.git develop –squash
```

## Contribute

How to [contribute](http://volttron.readthedocs.io/en/develop/contributing.html) back:

* Issue Tracker: http://github.com/VOLTTRON/volttron/issues
* Source Code: http://github.com/VOLTTRON/volttron

## Support
There are several options for VOLTTRONTM [support](http://volttron.readthedocs.io/en/master/community_resources/index.html#volttron-community).

* A VOLTTRONTM office hours telecon takes place every other Friday at 11am Pacific over Skype.
* A mailing list for announcements and reminders
* The VOLTTRONTM contact email for being added to office hours, the mailing list, and for inquiries is: volttron@pnnl.gov
* The preferred method for questions is through stackoverflow since this is easily discoverable by others who may have the same issue. http://stackoverflow.com/questions/tagged/volttron
* GitHub issue tracker for feature requests, bug reports, and following development activities http://github.com/VOLTTRON/volttron/issues

## License
The project is [licensed](TERMS.md) under a modified BSD license.
