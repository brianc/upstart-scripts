Scripts to start and manage processes with upstart

## generic-node

1. `sudo mkdir /srv`
2. `cd /srv`
3. `git clone https://github.com/(you)/(your_project).git`
4. `cd (your_project)`
5. `npm install`
6. `cd ~`
7. `git clone https://github.com/brianc/upstart-scripts.git`
8. `cd upstart-scripts`
9. `sudo ln -s generic-node.conf /etc/init/(your_project).conf`
10. `sudo initctl start (your_project)`

The script will start a node app by running `node /srv/(your_project)/index.js`

Right now you need node installed somewhere root can access it.  
To verify, make sure this return some valid output: `sudo which node`  

- It sets NODE_EVN=production
- It sets CWD to `/srv/(your_project)`
- It logs your processes stdout and stderr to `/var/log/(your_project).log`

That's really it.  Mostly here now because I keep having to reference it on other servers I set up.

you can stop your project with `sudo initctl stop (your_project)`  
you can restart your project with `sudo initctl restart (your_project)`

### warning
This will run your node application as __root__.  
You are responsible for dropping to a different user within the app.  
Use `process.setuid` and `process.setgid` [within node](http://nodejs.org/api/process.html#process_process_setuid_id).  
Or modify the script to use `setuid` and `setgid` [within upstart itself](http://upstart.ubuntu.com/cookbook/#setuid).
