# This is a Repository for developing to XYZ #

It will start a local REST Api running on localhost:3131/api/.

Documentation about the REST API can be found at [https://github.com/Softhouse/laughing-batman](https://github.com/Softhouse/laughing-batman "Laughing-batman")

To use this local api you need to follow these steps (assuming windows):

1. Install msysGit [https://msysgit.github.io/](https://msysgit.github.io/ "msysGit")
2. Install VirtualBox [https://www.virtualbox.org](https://www.virtualbox.org/wiki/Downloads "VirtualBox")
3. Install Ruby [http://rubyinstaller.org](https://rubyinstaller.org/downloads "Ruby Installer")
   - Check "Add Ruby executables to your PATH"
   - You can also check the other two options if you want, but it is not needed.
4. Install Ruby Devkit [http://rubyinstaller.org/](http://rubyinstaller.org/downloads "Ruby Installer")
   - Extract to some permanent location. I chose c:/Ruby22-x64/DevKit

    ```
    $ cd /c/Ruby22-x64/DevKit/
    $ ruby dk.rb init
    $ ruby dk.rb install
    ```

5. Install patched version of wdm

    ```
    $ git pull https://github.com/lowjoel/wdm
    $ cd wdm
    $ gem build wdm.gemspec
    $ gem install wdm-0.1.0.gem
    ```

6. Install Vagrant

    ```
    $ git clone https://github.com/mitchellh/vagrant.git
    $ cd vagrant
    $ gem install bundler -v 1.7.13
    $ bundle install
    $ rake install
    ```

7. Clone this repo

    ```
    $ git clone https://github.com/guzmo/xyz-docker-dev-api.git
    ```

Inside your local repository you need to create a file called **github_secret.env**.
The API uses this in production so it is needed here as well.

This file should only contain one row which is

    GITHUB_SECRET=THISISMYSUPERSECRET

If you have followed the above steps you should now be able to go to your
folder where you cloned this repo and execute:

    vagrant up

This will take a long time.  When it is done you can look in your
VirtualBoxManager and you should see a new box popup.

## Forward ports in VirtualBoxManager ##

When it has started you need to forward some ports to be able to reach the API on your machine.

This is done by selecting the newly created box and press settings.

To the left you should see a side bar, click Network.

In here you should see a button called something similiar to **Forward ports**, Click it!.

In the upper right corner there should be a plus sign, you know what to do with it.
Enter the credentials below:

    Host IP: 127.0.0.1
    Host Port: 3232 // Here you can choose the port of your choise
    Guest Port: 3232

And another one:

    Host IP: 127.0.0.1
    Host Port: 27017
    Guest Port: 27017

All done, you should now be able to reach the API in a browser or with curl on:

    localhost:3232/api

And the MongoDb instance that keeps all the data can be reached at
localhost:27017 (Try going there with a web browser and you should see "It
looks like you are trying to access MongoDB over HTTP on the native driver
port.")

## Troubleshooting ##

**Something goes wrong when you use *vagrant up:*** 

Use *vagrant destroy* to remove everything and then do *vagrant up* again.

**Error when docker containers are starting?**

Enter the Vagrant box by using the command *vagrant ssh* in the same folder as the Vagrantfile.
When inside:

    cd /vagrant
    docker-compose up

This should recreate the boxes and hopefully work.
