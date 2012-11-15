Scripts to start and manage processes with upstart

## generic-node

1. copy the file into `/etc/init/<your_process_name>.conf`
2. type `sudo initctl start <your_process_name>

The script will start a node app living at `/srv/<your_process_name>/index.js`

Right now you need node installed somewhere root can access it.  So, you'll need to make sure this return some valid output: `sudo which node`

It sets NODE_EVN=production

It logs your processes stdout and stderr to `/var/log/<your_process_name>.log`

That's really it.  Mostly here now because I keep having to reference it on other servers I set up.
