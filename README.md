# Important Links

- https://docs.travis-ci.com/user/database-setup/

- https://docs.travis-ci.com/user/languages/python/

# Travis.yml file using db

language: 

  - python

python:

  - "3.6"

postgres:

  - adapter: postgresql
  - database: test_db

services:

  - postgresql
  
before-script:

  - psql -c 'create database test_db;' -U postgres

install:
  - pip install -r requirements.txt
  - pip install coverage
  
script: 
  - coverage run -m unittest discover && coverage report
  
after_success:
  - coveralls

env:
 - DB=postgres
