# Failing Deployments

Deployments can fail; it could be a bad deployment script running before or after the deploy, or a bad script before activating the release. Or things can just go wrong, and Fuse didn’t have a way to know if a deployment failed. Time to address it.

One way to catch if a deployment failed is to use the exit code that the script to deploy a new release returns, because it uses a [callback](https://github.com/terrific-mx/fuse/blob/develop/resources/views/scripts/task-callback.blade.php) to let Fuse know the script has finished running, and along with that, it sends the [exit code](). So if the exit code is not successful, Fuse marks the deployment as failed.

There is another option to fail a deployment, and it’s useful if the server never makes the callback to Fuse when the script finishes. It’s on the [deploy site](https://github.com/terrific-mx/fuse/blob/develop/app/Jobs/DeploySite.php) job itself, where I check if the deployment is [stale](https://github.com/terrific-mx/fuse/blob/develop/app/Jobs/DeploySite.php#L41) by checking if the deployment was created more than 10 minutes ago and it’s still marked as deploying. It means it’s taking too long. So in that case, I mark the deployment as failed.

All these deployment statuses can be reviewed on the site deployments table to easily check which ones failed and which ones succeeded.