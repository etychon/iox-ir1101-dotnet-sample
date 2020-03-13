# Sample .NET application on Cisco IR1101

## Introduction

Let's get started by saying that running .NET applications at the edge is not something I'd recommend for a number of reasons:

* Edge applications need to be lightweight and fast, and typically run on a lightweight OS such as Linux, which is not ideal to run .NET
* .NET Core is very large and will greatly increase the size of your container, making it less agile, slower to deploy and start. As an example the rootfs.tar of this sample application, which only does "Hello World" is 778MB.
* Cisco IR1101 is a very efficient router with low power dissipation and runs ARM CPU, whereas .NET has been developed for Intel x86 and AMD64 architecture.

Nevertheless if you still want to go on despite those caveats, rest assured this is possible.

## Building

This project will be build using Microsoft provided [.NET Core SDK](https://hub.docker.com/_/microsoft-dotnet-core-sdk/) which is hosted on Docker Hub. From there you can find all the releases, for all the supported platforms.

For us to get started clone the current project with:

    git clone https://github.com/etychon/iox-ir1101-dotnet-sample.git
    cd iox-ir1101-dotnet-sample

Assuming you are building on x86 and have properly setup your QEMU environment to execute ARM binaries on x86, you can start building the image with:

    docker build -t iox-ir1101-dotnet-example  .

At this point, this should run on your local machine, but you can verify by running the container locally (be patient, it takes about 30 seconds to start on my machine):

![command](images/run-command.png)

If all is well, go on building the IOx application with:

    ioxclient docker package iox-ir1101-dotnet-example . -n iox-ir1101-dotnet-example --use-targz

The resulting file `iox-ir1101-dotnet-example.tar.gz` can be deployed to Cisco IOx using Local Manager or any other means. This is outside the scope of this example.
