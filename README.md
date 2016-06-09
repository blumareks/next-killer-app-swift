#Swift HelloWorld App Overview
This project contains a simple Swift hello world application that can be deployed to Bluemix or run locally on your [OS X](http://www.apple.com/osx/) or [Ubuntu Linux](http://www.ubuntu.com/download) system.  This sample application creates a basic server that returns an HTML greeting to the client.  Please note that this is not a production-ready application.  Instead, it is for educational purposes to learn about the types of applications you can develop using the Swift programming language.

## Application Requirements
To compile and run this sample application on your system, you need to install the [Swift compiler](https://swift.org/download/) for your platform. Please note that the Swift language is evolving and changing rapidly. The latest version of this Swift application works with the `DEVELOPMENT-SNAPSHOT-2016-05-03-a` version of the Swift binaries. You can download this version of the Swift binaries by following this [link](https://swift.org/download/).

If you are interested in manually deploying the application to Bluemix, you'd need to install the Cloud Foundry [command line](https://docs.cloudfoundry.org/devguide/cf-cli/install-go-cli.html) on your system.  Once it is installed, you can use it to [authenticate and access](https://www.ng.bluemix.net/docs/starters/install_cli.html) your Bluemix organization(s) and spaces.  You can find further details on how to deploy this sample application to Bluemix in the following sections.

## Run the app locally
Once you have installed the Swift compiler and cloned this Git repo, you can now compile and run the application. Go to the root folder of this repo on your system and issue the following command:
```
$ swift build
```
You should see an output similar to the following:
```
Compile Swift Module 'SwiftyJSON' (2 sources)
Compile Swift Module 'CloudFoundryEnv' (7 sources)
Compile Swift Module 'Utils' (6 sources)
Compile Swift Module 'Server' (1 sources)
Linking .build/debug/Server
```
Once the application is successfully compiled, you can run the executable that was generated by the Swift compiler:
```
$ .build/debug/Server
```
You should see an output similar to the following:

```
Server is listening on port: 8090
```

To connect to the server, you can use the browser of your preference (e.g. Firefox, Chrome, etc.) to point to the following URL: `http://<hostname>:8090/`, where `<hostname>` is the hostname or the IP address of the system where you are running the sample app.  If the browser is running on the same system, you can use localhost as the value for the hostname.  After you access the server, the browser should render an HTML page with the following message:

```
Hello from Swift on Linux!
```

Below the greeting message, you should also see an HTML table that displays the environment variables for the app.

## Running the app on Bluemix
### Using the magical button
Click the magical button below to automatically deploy this sample application to Bluemix.

[![Deploy to Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy)

When automatically deploying to Bluemix, the manifest.yml file [included in the repo] is parsed to obtain the name of the application.  For further details on the structure of the manifest.yml file, see the [Cloud Foundry documentation](https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html#minimal-manifest).

### Using the Cloud Foundry command line
You can also manually deploy the app to Bluemix.  Though not as magical as using the Bluemix button above, manually deploying the app gives you some insights about what is happening behind the scenes.  Remember that you'd need the Cloud Foundry [command line](https://www.ng.bluemix.net/docs/starters/install_cli.html) installed on your system to deploy the app to Bluemix.

Using the Cloud Foundry command line you can get a list of the buildpacks (along with their versions) that are installed on Bluemix.

```
cf buildpacks
```

Executing the above command should result in output similar to the following:

```
Getting buildpacks...

buildpack                                 position   enabled   locked   filename   
liberty-for-java                          1          true      false    buildpack_liberty-for-java_v2.9-20160519-1249.zip   
sdk-for-nodejs                            2          true      false    buildpack_sdk-for-nodejs_v3.4-20160518-1653.zip   
noop-buildpack                            3          true      false    noop-buildpack-20140311-1519.zip   
java_buildpack                            4          true      false    java-buildpack-v3.5.1.zip   
ruby_buildpack                            5          true      false    ruby_buildpack-cached-v1.6.9.zip   
nodejs_buildpack                          6          true      false    nodejs_buildpack-cached-v1.5.3.zip   
go_buildpack                              7          true      false    go_buildpack-cached-v1.7.0.zip   
python_buildpack                          8          true      false    python_buildpack-cached-v1.5.2.zip   
php_buildpack                             9          true      false    php_buildpack-cached-v4.3.0.zip   
swift_buildpack                           10         true      false    swift_buildpack-cached-v1.1.1.zip   
aspnet5-experimental                      11         true      false    buildpack_aspnet5-experimental_v0.7-20151022-1257.zip   
xpages_buildpack                          12         true      false    xpages_buildpack_v1.1.1-20160518-0936.zip   
aspnet5-experimental_v0_6-20150916-1220   13         true      false    buildpack_aspnet5-experimental_v0.6-20150916-1220.zip   
liberty-for-java_v2_3-20151208-1311       14         true      false    liberty-for-java_v2.3-20151208-1311.zip   
sdk-for-nodejs_v3_3-20160428-1409         15         true      false    buildpack_sdk-for-nodejs_v3.3-20160428-1409.zip   
liberty_for_java_v2_8-20160430-1011       16         true      false    buildpack_liberty-for-java_v2.8-20160430-1011.zip   
xpages_buildpack_v1_0_0-20160310-1442     17         true      false    xpages_buildpack_v1.0.0-20160310-1442.zip   
swift_buildpack-cached-v1_0_3             18         true      false    swift_buildpack-cached-v1.0.3.zip
```

Looking at the output above, we can see that the Swift buildpack (v1.1.1) is installed on Bluemix.  This will allow a seamless deployment of the starter application to Bluemix. After you have cloned this Git repo, go to its root folder on your system and issue the following command Cloud Foundry command:

```
cf push
```

Executing the Cloud Foundry push command will parse the contents of the manifest.yml file and upload the application to Bluemix.  This action should generate an output similar to the following:

```
Using manifest file /Users/olivieri/git/swift-helloworld/manifest.yml

Creating app swift-helloworld in org john_doe@us.ibm.com / space dev as john_doe@us.ibm.com...
OK

Creating route swift-helloworld-shadowgraphic-insomnolence.mybluemix.net...
OK

Binding swift-helloworld-shadowgraphic-insomnolence.mybluemix.net to swift-helloworld...
OK

Uploading swift-helloworld...
Uploading app files from: /Users/olivieri/git/swift-helloworld
Uploading 46.8K, 18 files
Done uploading               
OK

Starting app swift-helloworld in org john_doe@us.ibm.com / space dev as john_doe@us.ibm.com...
-----> Downloaded app package (20K)
-----> Installing system level dependencies...
Ign http://archive.ubuntu.com trusty InRelease
Get:1 http://archive.ubuntu.com trusty-updates InRelease [65.9 kB]
Get:2 http://archive.ubuntu.com trusty-security InRelease [65.9 kB]
Get:3 http://archive.ubuntu.com trusty Release.gpg [933 B]
Get:4 http://archive.ubuntu.com trusty Release [58.5 kB]
Get:5 http://archive.ubuntu.com trusty-updates/main amd64 Packages [970 kB]
Get:6 http://archive.ubuntu.com trusty-updates/universe amd64 Packages [467 kB]
Get:7 http://archive.ubuntu.com trusty-updates/multiverse amd64 Packages [14.3 kB]
Get:8 http://archive.ubuntu.com trusty-security/main amd64 Packages [609 kB]
Get:9 http://archive.ubuntu.com trusty-security/universe amd64 Packages [169 kB]
Get:10 http://archive.ubuntu.com trusty-security/multiverse amd64 Packages [4,853 B]
Get:11 http://archive.ubuntu.com trusty/main amd64 Packages [1,743 kB]
Get:12 http://archive.ubuntu.com trusty/universe amd64 Packages [7,589 kB]
Get:13 http://archive.ubuntu.com trusty/multiverse amd64 Packages [169 kB]
Fetched 11.9 MB in 8s (1,398 kB/s)
Reading package lists...
       Reading package lists...
       Building dependency tree...
       The following extra packages will be installed:
         libblocksruntime0 libssl1.0.0
       Recommended packages:
         libssl-doc
       The following NEW packages will be installed:
         libblocksruntime-dev libblocksruntime0 libkqueue0
       The following packages will be upgraded:
         libssl-dev libssl1.0.0 openssl
       3 upgraded, 3 newly installed, 1 reinstalled, 0 to remove and 103 not upgraded.
       Need to get 2,600 kB of archives.
       After this operation, 229 kB of additional disk space will be used.
       Get:1 http://archive.ubuntu.com/ubuntu/ trusty-updates/main libssl-dev amd64 1.0.1f-1ubuntu2.19 [1,073 kB]
       Get:2 http://archive.ubuntu.com/ubuntu/ trusty-updates/main libssl1.0.0 amd64 1.0.1f-1ubuntu2.19 [828 kB]
       Get:3 http://archive.ubuntu.com/ubuntu/ trusty-updates/main libcurl3 amd64 7.35.0-1ubuntu2.6 [172 kB]
       Get:4 http://archive.ubuntu.com/ubuntu/ trusty-updates/main openssl amd64 1.0.1f-1ubuntu2.19 [490 kB]
       Get:5 http://archive.ubuntu.com/ubuntu/ trusty/universe libblocksruntime0 amd64 0.1-1 [8,128 B]
       Get:6 http://archive.ubuntu.com/ubuntu/ trusty/universe libblocksruntime-dev amd64 0.1-1 [4,660 B]
       Get:7 http://archive.ubuntu.com/ubuntu/ trusty/universe libkqueue0 amd64 1.0.4-2ubuntu1 [23.4 kB]
       Fetched 2,600 kB in 3s (750 kB/s)
       Download complete and in download only mode
-----> Downloaded DEB files...
-----> Installing libblocksruntime0_0.1-1_amd64.deb
-----> Installing libblocksruntime-dev_0.1-1_amd64.deb
-----> Installing libcurl3_7.35.0-1ubuntu2.6_amd64.deb
-----> Installing libkqueue0_1.0.4-2ubuntu1_amd64.deb
-----> Installing libssl1.0.0_1.0.1f-1ubuntu2.19_amd64.deb
-----> Installing libssl-dev_1.0.1f-1ubuntu2.19_amd64.deb
-----> Installing openssl_1.0.1f-1ubuntu2.19_amd64.deb
-----> Writing profile script...
-----> Buildpack version 1.1.1
-----> Installing Swift DEVELOPMENT-SNAPSHOT-2016-05-03-a
       Downloaded Swift
-----> Installing Clang 3.7.0
       Downloaded Clang
-----> Adding libdispatch binaries...
-----> Building Package...
       Cloning https://github.com/IBM-Swift/Swift-cfenv.git
       Resolved version: 1.1.0
       Cloning https://github.com/IBM-Swift/SwiftyJSON.git
       Resolved version: 7.0.4
       Compile SwiftyJSON
       Compile CloudFoundryEnv
       Compile Utils
       Compile Server
       Linking .build/release/Server
-----> Copying dynamic libraries
-----> Copying binaries to 'bin'
-----> Cleaning up build files

-----> Uploading droplet (9.4M)

0 of 1 instances running, 1 starting
1 of 1 instances running

App started


OK

App swift-helloworld was started using this command `Server`

Showing health and status for app swift-helloworld in org john_doe@us.ibm.com / space dev as john_doe@us.ibm.com...
OK

requested state: started
instances: 1/1
usage: 128M x 1 instances
urls: swift-helloworld-shadowgraphic-insomnolence.mybluemix.net
last uploaded: Wed Jun 8 18:47:30 UTC 2016
stack: unknown
buildpack: Swift

     state     since                    cpu    memory          disk          details   
#0   running   2016-06-08 01:51:07 PM   0.0%   12.1M of 128M   34.1M of 1G      
```

Once the sample application is pushed to Bluemix, you can access it using its route. You can log on to your [Bluemix account](https://console.ng.bluemix.net) to find the route of your application or you can inspect the output from the execution of the `cf push` command.  The string value (e.g. swift-helloworld.mybluemix.net) shown next to the urls should contain the route.  Use that route as the URL to access the sample server using the browser of your choice.  The browser should render an HTML page with the following message at the top:

```
Hello from Swift on Linux!
```

## Using a different version of Swift on Bluemix for your application
If you look closely at the output above returned by the `cf push` command, you will notice that `DEVELOPMENT-SNAPSHOT-2016-05-03-a` was the Swift version used for compiling and running the sample app on Bluemix.  If you have a Swift application that compiles with a different version of the Swift binaries, say `DEVELOPMENT-SNAPSHOT-2016-04-25-a`, you'd need to update the contents of the `.swift-version` file to:

```
DEVELOPMENT-SNAPSHOT-2016-04-25-a
```

After updating the `.swift-version` file, you can run the `cf push -b https://github.com/IBM-Swift/swift-buildpack` command.  Note that if using a version of the Swift binaries other than `DEVELOPMENT-SNAPSHOT-2016-05-03-a`, you'd need to add the `-b https://github.com/IBM-Swift/swift-buildpack` parameter for the execution of the `push` command.  This action should upload your application to Bluemix and use the `DEVELOPMENT-SNAPSHOT-2016-04-25-a` version of the Swift binaries for compiling and running your application as shown.

For a complete list of the Swift versions currently supported by the Swift buildpack for Bluemix, see the buildpack's [manifest](https://github.com/IBM-Swift/swift-buildpack/blob/bluemix-buildpack/manifest.yml) file.  If you cannot find the version of the Swift binaries you are looking for in this file, then that version is not currently supported.

## What's next?
As new releases of the Swift binaries are made available at (Swift.org)[https://swift.org/], our team will update the (Swift buildpack)[https://github.com/IBM-Swift/swift-buildpack] for Bluemix.  Also, our team is currently working on a much more advanced version of this HTTP server that will be available soon.  We also plan to provide Swift packages that will allow developers communicate with middleware services such as CouchDB and Cloudant.  Stay tuned for updates!
