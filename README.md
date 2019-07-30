# NeoLoad TeamCity Example
A simple example of using Docker-based controllers as TeamCity agents to run small load tests continuously.

Current TeamCity Agent version is at 66192, but you can change Dockerfile ADD to support your specific version, available from your TeamCity dashboard as admin: Agents > Zip file distribution.

DISCLAIMER: this example only covers Docker-based controllers and a simple example of how to execute a small test as a TeamCity build agent. There are other options, such as using NeoLoad Web Runtime and OpenShift containers to execute tests without having to handle controller and load generator infrastructure in your pipeline.

**Initializing Your Agents**

 - Clone this repo, cd into 'neoload-controller-teamcity' subdirectory
 - rename the 'rename_to_agents' directory to 'agents'
 - for each agent (could be multiple), copy the 'replace_with_agent_name' and rename it to match the agent name to be visible in TeamCity (must be unique of course)
 - change each agent conf/buildAgent.properties to have your server URL and the unique agent name
 - update the Docker Compose 'neoload-compose.yaml' file to match your agent name(s)

**Running Docker Compose**
```
SERVER_URL=http://[teamcity_host]:[port] docker-compose --file neoload-compose.yaml up --remove-orphans
```

**Running a NeoLoad Performance Test in TeamCity**

[Official Neotys Docs](https://www.neotys.com/documents/doc/neoload/latest/en/html/#24781.htm)

 - Pull a NeoLoad project in via Git as a first job step
   - typically this would go in a subfolder of it's own, such as 'nl_project'
 - Add a second step for running the NeoLoad test
   - NeoLoad executable path is: /home/neoload/neoload/bin/NeoLoadCmd
   - Don't forget to add additional command line arguments to ship stats up to NeoLoad Web:
        ```-nlweb -nlwebToken a8e8f0c5a4f90c02bfddcb6881e7f6811da26864879a7bd6```
