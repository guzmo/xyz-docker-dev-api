# This is a Repository for developing to XYZ #

It will start an local REST Api running on localhost:3131/api/.

Documentation about the REST API can be found at [https://github.com/Softhouse/laughing-batman](https://github.com/Softhouse/laughing-batman "Laughing-batman")

To use this local api you need to install:

1.  Vagrant [https://www.vagrantup.com/](https://www.vagrantup.com/ "Vagrant")
2.  VirtualBox Manager [http://www.oracle.com/technetwork/server-storage/virtualbox/downloads/index.html](http://www.oracle.com/technetwork/server-storage/virtualbox/downloads/index.html "VM Manager")

Inside your local repository you need to create a file called **github_secret.env**.
The API uses this in production so it is needed here as well.

This file should only contain one row which is

    GITHUB_SECRET=THISISMYSUPERSECRET

If you have followed the above steps you should now be able to go to your folder where you cloned this repo and execute:

    vagrant up

If you now look in your VirtualBoxManager you should see a new box popup.

## Forward ports in VirtualBoxManager ##
When it has started you need to forward some ports to be able to reach the API on your machine.

This is done by selecting the newly created box and press settings.

To the left you should see a side bar, click Network.

In here you should see a button called something similiar to **Forward ports**, Click it!.

In the upper right corner there should be a plus sign, you know what to do with it.
Enter the credentials below:


    Host IP: 127.0.0.1
    Host Port: 3131 // Here you can choose the port of your choise
    Guest Port: 8080

All done, you should now be able to reach the API in a browser or with curl on:

    localhost:3131/api


## Troubleshooting ##


**Something goes wrong when you use *vagrant up:*** 

Use *vagrant destroy* to remove everything and than do *vagrant up* again.

**Error when docker containers are starting?**

Enter the Vagrant box by using the command *vagrant ssh* in the same folder as the Vagrantfile.
When inside:

    cd /vagrant
    docker-compose up

This should recreate the boxes and hopefully work.
