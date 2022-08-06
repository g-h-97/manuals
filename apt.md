
# Kill apt

This may happen if

    'Synaptic Package Manager' or 'Software Updater' is open.

    Some apt command is running in Terminal.

    Some apt process is running in background.

For above wait for the process to complete. If this does not happen run in terminal:

sudo killall apt apt-get

If none of the above works, remove the lock files. Run in terminal:

sudo rm /var/lib/apt/lists/lock
sudo rm /var/cache/apt/archives/lock
sudo rm /var/lib/dpkg/lock*

then reconfigure the packages. Run in terminal:

sudo dpkg --configure -a

and

sudo apt update

That should do the job.

# apt FrontEnds (For Automated Installed and Such)

https://www.cyberciti.biz/faq/explain-debian_frontend-apt-get-variable-for-ubuntu-debian/

> DEBIAN_FRONTEND=noninteractive
