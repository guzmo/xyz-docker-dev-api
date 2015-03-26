# This is a Repository for developing to XYZ #

It will start a local REST Api running on localhost:3232/api/.

Documentation about the REST API can be found at [https://github.com/Softhouse/laughing-batman](https://github.com/Softhouse/laughing-batman "Laughing-batman")

## Linux 
1. Clone this repo.

    ```
    $ git clone https://github.com/guzmo/xyz-docker-dev-api.git
    ```

2. Start docker deamon.

	```
    $ sudo docker -d 
    ```

3. Run docker-comepose.sh

	```
    $ ./docker-compose.sh
    ```

4. Start docker

	```
    $ sudo docker-compose up
    ```

## Windows/Mac

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
    $ git clone https://github.com/lowjoel/wdm
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
The API uses this in production so it is needed here as well. **Secret can be anything during development**.

This file should only contain one row which is

    GITHUB_SECRET=THISISMYSUPERSECRET

If you have followed the above steps you should now be able to go to your
folder where you cloned this repo and execute:

    vagrant up

This will take a long time.  When it is done you can look in your
VirtualBoxManager and you should see a new box popup.

## Test your setup ##

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

**Other errors**

If you get this error below: 

    ==> default: Waiting for machine to boot. This may take a few minutes...
    The guest machine entered an invalid state while waiting for it
    to boot. Valid states are 'starting, running'. The machine is in the
    'poweroff' state. Please verify everything is configured
    properly and try again.

or if you get timeout or ssh problems to the box, the cause may be Virtualizaion(VT-x) being turned off in the BIOS.

