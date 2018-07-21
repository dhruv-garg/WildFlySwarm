WildFly Swarm for MicroServices

WildFly emerged as an enterprise-capable open source application server.

WildFlySwarm is a complete teardown of the WildFly application server into bite-sized, reusable components called fractions that can be assembled and formed into a microservice application that leverages Java EE API's.

Getting Started: 

Three ways to get started with WildFLy Swarm-
1) Blank Java Maven or Gradle Project.
2) WildFly Swarm Generator web console.
   Link:- http://wildfly-swarm.io/generator/
3) JBoss Forge tool.
   Probably the most cool one.

This procedure is written in context of JBoss Forge tool.

Installation:

Download JBoss Forge (Linux Version) : https://forge.jboss.org/download

Untar the file and run forge located in bin folder.
Prerequisites: Make sure that Java 8 or above is installed.

Basic Run Commands:
-> forge
-> addon-install \ 
   --coordinate org.jboss.forge.addon:wildfly-swarm,1.0.0.Beta2
The above command installs the WildFly Swarm addon for JBoss Forge.

Now, let's create a project:
-> project-new
This command prompts for some input
   Project-name: widlfyswarm-demo
   Top level package: com.redhat.examples.wfswarm
   Version: 1.0
   Final name: wildflyswarm-demo
   Project location: Press enter
   Project type: [0-7]
   Build System: [0]
   Stack (The technology stack to be used in project): [0-2] 2

If you followed all the steps correctly then output shoudl look like:
   ***SUCCESS*** Project named 'wildflyswarm-demo' has been created.
If not, steps need to recheked again.

Let's set it up for a JAX-RS application:
-> rest-setup --application-path=/
Desired output:
    ***SUCESSS*** JAX_RS has been installed

Let's add in the wildfly swarm configs like the Maven plug-in an the BOM dependency management section:
-> wildfly-swarm-setup --context-path=/

That's it! Now let's build and try to run our new WildFly Swarm microservice:
-> cd ~~
-> wildfly-swarm-run

We can see it successfully being start, but it doesn't do anything or eexpose any REST services.
If we are considerate about what JBoss forge did for us, we could have a look at the directory structure and the pom.xml file it created for us.

Let's add some basic functionality to it.

-> forge
Run forge if it is not already running
-> rest-new-endpoint
Desired Output: ***INFO*** Required inputs not satisfied, interactive mode
-> ?Package Name: press enter
-> Type Name: Enter java file name to be created
-> Press Enter to confirm
-> Path (The root path of the endpoint): api/hello
Desired Output: ***SUCCESS***
REST com.dhruv.examples.wfswarm.rest.NewResource created

After this process, a new java class named NewResource should be created and should be exposed to the path we mentioned.
Great, isn't it?

Let's fire it up again:
-> cd ~~
-> wildfly-swarm-run

Navigate to a browser and type http://localhost:8080/api/hello

What we did in the whole process was, we built a JAX-RS web applicationusing native Java EE with the JBoss Forge tooling and then ran it as a microservice inside WildFlySwarm.
