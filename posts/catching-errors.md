# Catching provisioning errors

Not always does provisioning a new server run as expected, and so far, Fuse hasn’t provided any feedback about when an error emerges or if it fails the provisioning, so the provisioning status can hang forever. It’s time to address this.

The first thing is that we shouldn’t provision a server that has already been provisioned. When a server is provisioned, it finalizes the task with a callback to Fuse to change the server status from provisioning to provisioned. So, with an accessor, Fuse just checks that the server hasn’t been provisioned; if so, the Laravel server provisioner job is deleted.

Next, if the server is already provisioning, then the server status is provisioning, which means that the script to provision the server has not finished yet. In that case, the server provisioner job is released for 30 seconds to check the server status again.

Now it’s time to know what to do with servers that haven’t finished the provisioning script for too long. So, Fuse checks when the server was created, and if it’s older than 15 minutes, it means that something wrong happened and it should be marked as a failing task.

Then, it’s time to adjust what the maximum time to wait before failing the provisioning job is. I have set it up for 40 tries, which means a total of 20 minutes provisioning a server.

When a failed provisioning occurs, it automatically deletes the server. But the server itself is still active, so you can check the server logs to review the log of the provisioning script and debug the issue. Hopefully, this happens very few times.