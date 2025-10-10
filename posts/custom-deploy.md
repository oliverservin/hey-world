# Not all app deployments are the same

At [Fuse](http://fuse.terrific.com.mx), each new site created has an opinionated zero-downtime deployment flow that works for most basic Laravel applications. But not all application deployments are the same, and from now on, they can be customized.

Because Fuse uses a zero-downtime deployment approach, you must first declare which directories and files can be shared across deployments. For most apps, this means sharing the storage directory and the environment file, .env, to make them persist across deployments. If your app uses SQLite, you may want to declare the database/database.sqlite file path as a shared file.

Then you must make sure that certain directories can be writable by the application, mostly the storage directory that stores sessions, cache, and compiled views, but also logs, and the public and private local storage used by Laravel.

These shared and writable directories and files can be declared in a way that every line break is a new item. Fuse actually stores this data in an array, but to make it easier to configure, it presents you the lists as a [string](https://github.com/terrific-mx/fuse/blob/develop/app/Livewire/Forms/DeploymentSettingsForm.php#L37) with line breaks, and then it’s converted to [arrays](https://github.com/terrific-mx/fuse/blob/develop/app/Livewire/Forms/DeploymentSettingsForm.php#L51) just before storing the new settings.

The next section configurable is the scripts to be run at certain stages of the deployment flow. You can customize the scripts to be run just before updating the Git repository and after updating the Git repository. Also, the scripts to be run before activating the new deployment release and also after activating the release.

For most applications, the script to be run before activating the release is the one that you may want to customize. By default, it installs your Composer dependencies, your npm dependencies, runs the build command to compile your assets, and executes artisan commands to make sure your application is production-ready, like running the configuration, route, view, and event cache. Here you may want to also run your application’s [migrations](https://laravel.com/docs/12.x/migrations#running-migrations).

On the after-activating release script, if your application uses queues, you can use the artisan command to [restart](https://laravel.com/docs/12.x/queues#queue-workers-and-deployment) the queues and reload the PHP FPM service to ensure it uses the latest deployed code. Personally, I also use [Honeybadger](https://www.honeybadger.io) as my error reporting tracker, so my script runs the honeybadger:deploy command to inform Honeybadger of the new deployment.

All these configurations are probably the ones you may want to use for your deployment settings to match your deployment application requirements. Or you can just stick with the default ones. It’s up to you, but you have the option to configure it now.

By the way, all fields in the deployment settings page have descriptions to describe their purpose, and as a final UX touch, the servers item in the sidebar navigation is displayed as an active item on all server URL paths, just a minor quality of life improvement.