# Let me know what’s the status, without refreshing

[Fuse](http://fuse.terrific.com.mx) uses the Laravel Queues system internally to dispatch jobs for provisioning. This means the work is offloaded, and you, as a user, don’t really know if the status of the server has changed to provisioned unless you refresh the page.

That’s not good; you want to always know what the latest status is without refreshing the page.

There are different approaches to tackle this problem, but the easiest one, since Fuse uses Livewire, is the [polling](https://livewire.laravel.com/docs/wire-poll) method to automatically [refresh](https://github.com/terrific-mx/fuse/commit/c86e44956ee7cf5d5d4e45fc38586a25cce9a5c0#diff-48e8d71e0d1932c64cc57edea9c8e9fd11da1b24fe788d09aea2266f4d4207e2R63) the servers table after 2.5 seconds. No more manually refreshing the page.

And since I was already working on server statuses, I have refreshed them to show them as Flux [badges](https://fluxui.dev/components/badge) with a dynamic color: green for successfully provisioned and blue for provisioning. I also took the liberty to apply a “pulse” Tailwind CSS class so you get a little UI feedback to know this is a progress status. It’s a nice touch to know that something is still in progress and working on it.

This approach also applies to the deployments table, so now it automatically refreshes the table to get the most updated deployment status with a similar status color system.

Lastly, since I expect you to ship more often, I have added [pagination](https://github.com/terrific-mx/fuse/commit/acac4764c9350329ac13265061f24cfb0d9f0a54#diff-69a1c17e6d54e4ce26c16c9fa2d57cdbb60b7944a07c879586d6c442ddc6d35bR62) to the deployments table. I know you will be deploying your app hundreds, if not thousands, of times. And that’s great; keep shipping.