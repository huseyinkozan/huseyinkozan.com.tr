# huseyinkozan.com.tr

## Clone

* Clone this repo with submodules:
  ```
  git clone --recursive https://github.com/huseyinkozan/huseyinkozan.com.tr.git
  ```

## Install

* Install docker and docker-compose from official docs
* Install _npm_ packages:
  ```
  npm i -g hexo
  cd <path/of/this/repo>
  npm i
  ```
* Generate static website:
  ```
  hexo generate
  ```
* Create files dir:
  ```
  mkdir ~/files
  cd <path/of/this/repo>
  mkdir -p public/files
  ```
* Create .env file:
  ```
  cd <path/of/this/repo>
  cp .env.sample .env
  nano .env
  ```

## Run

* Serve HTTP:
  ```
  hexo server
  ```
* Serve HTTPS:
  ```
  docker-compose up
  ```

## Setup DNS Server

* Open https://<IP>:10000.
* Servers > BIND DNS Server > Setup RNDC > Yes (be patient)
* Servers > BIND DNS Server > Create Master Zone
* ...
* Servers > BIND DNS Server > Zone Defaults > Allow queries from.. > Listed ... > `any`
* Servers > BIND DNS Server > Addresses and Topology > Ports and addresses to listen on > Listed below.. > Port=`53`, Addresses=`any`
* Servers > BIND DNS Server > Apply
* Servers > BIND DNS Server > Stop (be patient, refresh if needed)
* Servers > BIND DNS Server > Start

Resource : https://www.youtube.com/watch?v=PBMQVsoEgik


## Host DNS Conf

`sudo nano /etc/dhcp/dhclient.conf`:
```
#...
supersede domain-name-servers 127.0.0.1
#...
```

```
sudo dhclient -r && dhclient
sudo service docker restart
```

`sudo nano /etc/docker/daemon.json`:
```
{
    "dns": ["127.0.0.1"]
}
```

```
sudo service docker restart
```


## TODO

* Switch to `hexo-renderer-pug`.
