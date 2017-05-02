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

## Run

* Serve HTTP:
  ```
  hexo server
  ```
* Serve HTTPS:
  ```
  docker-compose up
  ```

## TODO

* Switch to `hexo-renderer-pug`.
