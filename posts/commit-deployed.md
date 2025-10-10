# What commit was deployed

Wouldn’t it be nice to know what commit was deployed? Well, I just shipped it. Now, on the deployments table, you can see the [commit hash](https://github.com/terrific-mx/fuse/blob/develop/resources/views/livewire/servers/sites/deployments.blade.php#L65) that was deployed, so you can see what the latest commit deployed from your Laravel app is.

When a deployment script [finalizes](https://github.com/terrific-mx/fuse/blob/develop/app/Models/Server.php#L147), it does a callback to Fuse to update the deployment status to [deployed](https://github.com/terrific-mx/fuse/blob/develop/app/Callbacks/UpdateDeploymentStatus.php#L19), but now it also [runs](https://github.com/terrific-mx/fuse/blob/develop/app/Models/Deployment.php#L145) a script to get the latest hash from the latest deployed releases of your Laravel app.

It basically uses the command [git rev-list](https://github.com/terrific-mx/fuse/blob/develop/app/Models/Server.php#L163) to get the latest commit from your deployed branch, and then Fuse [updates](https://github.com/terrific-mx/fuse/blob/develop/app/Models/Deployment.php#L147) the deployment commit with the returned hash.

The hash can be a bit long, so in the table, it only shows the shorter commit hash with the [first 7 characters](https://github.com/terrific-mx/fuse/blob/develop/app/Models/Deployment.php#L155).

So now, you can tell what the latest commit deployed of your Laravel app is.