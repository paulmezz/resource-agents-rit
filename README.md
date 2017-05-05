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

There are a bunch of 'logger' commands jammed into this resource agent right now
so I can track down an issue where the locks exist, but the check fails.  It
appears that lvmlockctl does NOT always work.  This is a BadThing(tm) when
dealing with pacemaker.  I switched to the much more dirty feeling
/sys/kernel/debug/dlm method and it has been rock solid.  This does require
debugfs to be either in the kernel or loaded as a module.  No guarantees
on how portable this check is.  I need to find a better check for this.

Follow my directions with the knowledge that I am still figuring this out myself

# ToDo:
Initially this was based off a one-shot script used internaly.  It didn't need 
any checks so it didn't have any.  Since I'm actually making this 'real' it 
needs all the checks filled out correctly.


