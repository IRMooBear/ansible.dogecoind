[![Build Status](https://travis-ci.org/IRMooBear/ansible.dogecoind.svg?branch=master)](https://travis-ci.org/IRMooBear/ansible.dogecoind)

Dogecoind
=========

This ansible role compile dogecoin core on RPI.

**I no longer recommend running this on an RPI.  The limited RAM causes too many crashes leading to reindex and more crashes.  You can build it, but it wouldn't run very well.**

Requirements
------------

This role is dependent upon BerkeleyDB being present.
You can compile it and link then set the dogecoind_bdb_prefix variable
or just download my role "berkeleydb" from ansible galaxy.

Dogecoind even on absolute minimal settings required some 500+ MB of RAM for a total of slightly 
over 650MB RAM usage on an RPI.  Only use this tool with at least a Pi 3B or Pi 3B+.

I highly recommend you also boot from a USB SSD and have at least 2GB of swap file set up.  Compiling this role with
j4 on an RPI with 4GB of swap took about 2 hours and swap space usage spiked up to 2GB+ during compile.

Role Variables
--------------
This set the j flag during make.  Suggest setting this to 4, otherwise it might take a while.

    compile_threads: 1
    
Version in git being checked out.
    
    dogecoind_version: v1.14-beta-1

Local standalone Berkeley DB location.

    dogecoind_bdb_prefix: /usr/local/BerkeleyDB.5.1
    
Default dir for data storage.    
    
    dogecoind_datadir: /var/lib/dogecoind
    
These are the default variables for dogecoind template generation.  You can read the dogecoin.conf man file for more. 
    
    dogecoind_user: dogecoin
    dogecoind_group: dogecoin
    dogecoind_testnet: 0
    dogecoind_server: 1
    dogecoind_txindex: 1
    dogecoind_maxconnections: 4
    dogecoind_rest: 1
    dogecoind_dbcache: 64
    dogecoind_disablewallet: 1
    dogecoind_maxmempool: 32
    dogecoind_par: 4
    dogecoind_listen: 0
    dogecoind_rpcconnect: 127.0.0.1
    dogecoind_rpcallowip: 192.168.0.0/16
    dogecoind_rpcuser: dogecoinrpc
    dogecoind_rpcpassword: dogecoin

Dependencies
------------

- irmoobear.berkeleydb

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: irmoobear.dogecoind }

Usage
-----

    sudo service dogecoin start
    sudo systemctl start dogecoin

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
