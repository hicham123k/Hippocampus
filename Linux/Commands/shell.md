# File & directory management

ls → list files

cd → change directory

mkdir → create a directory
create multiple dirs in one go:  mkdir -p /intranet/uplouds

rm → remove files/directories

# User & permission management
add user:    $sudo adduser editor
create group:  $sudo addgroup grpnet
add users to a group:   sudo gpasswd editor,viewer,admin grpnet

whoami → show current user

groups → show group membership

chown → change ownership
set ownership to a certain group and root: sudo shown :grpnet /intranet/uplouds  the ownership of the 2 dirs set to the group grpnet and the root,':' means with the root.

chmod → change permissions

System monitoring

top → show running processes

df -h → check disk space

free -m → check memory usage

Networking

ping → test connection

curl / wget → download files