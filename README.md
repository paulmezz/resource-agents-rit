# resource-agents-rit
Pacemaker Resource agents that we use at RIT (in RHEL 7.x).   

# ocf:ceph:rbd.in 
This is from github ceph/ceph.  I haven't made any changes and I just have 
a copy here to make it easier for me.

# ocf:rit:EnableLocksActivateVG
This is the one I'm actively working on.  It turns out that lvmlockd is the 
way forward, but some of the connective bits aren't quite there yet.

So far, this is what works: 
in lvm.conf, leave lvmetad enabled and enable lvmlockd.
Make a shared volume group on your shared block device (we are using ceph).
Activate the VG
Use the VG.

I'm actively working on figuring out the best way to make all this work.
Follow my directions with the knowledge that I have no idea what I'm doing.....
yet

# ToDo:
Initially this was based off a one-shot script used internaly.  It didn't need 
any checks so it didn't have any.  Since I'm actually making this 'real' it 
needs all the checks filled out correctly.


