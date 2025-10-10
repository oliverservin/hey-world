# Better deployment monitoring

When a new deployment is triggered, Fuse dispatches a [DeploySite](https://github.com/terrific-mx/fuse/blob/develop/resources/views/livewire/servers/sites/deployments.blade.php#L38) job; however, there was no way to monitor the deployment, like when the deployment script was run for too long without marking the deployment as successful.

For that reason, I have improved the job to actually monitor the deployment status.

First, by checking that if the deployment has been marked as [deployed](https://github.com/terrific-mx/fuse/blob/develop/app/Jobs/DeploySite.php#L24), Fuse [deletes](https://github.com/terrific-mx/fuse/blob/develop/app/Jobs/DeploySite.php#L25) the job.

If the deployment is still being [deployed](https://github.com/terrific-mx/fuse/blob/develop/app/Jobs/DeploySite.php#L30), Fuse releases the job to check the deployment status again in [30 seconds](https://github.com/terrific-mx/fuse/blob/develop/app/Jobs/DeploySite.php#L31).

Now it’s time to check for long-running deployments. For that case, I have decided that deployments that were created more than [10 minutes ago](https://github.com/terrific-mx/fuse/blob/develop/app/Models/Deployment.php#L94) are [stale](https://github.com/terrific-mx/fuse/blob/develop/app/Jobs/DeploySite.php#L36), so Fuse should [fail](https://github.com/terrific-mx/fuse/blob/develop/app/Jobs/DeploySite.php#L37) the deployment job.

I love this approach since I can use the same DeploySite job to monitor the deployment and run the server deployment script on the server.

I also kept the Job class skinny by moving status checks to the Deploy model. I especially love the check isStale method name, as it perfectly describes stale deployments and it just checks if the deployment was created more than 10 minutes ago.