# Launching a SaaS is only the beginning

Only a few hours have passed since I launched Fuse, and I continue shipping improvements.

Let’s be honest, I was a bit in a hurry to launch Fuse; I needed to stop working only locally and actually ship it to the world. However, it means that a few things were not optimal: the UI was not clear, and UI copy was missing, but at least it’s open to the public.

But now, it’s time to amend at least a few of those issues.

I started by moving all the forms to add SSH keys, servers, and sites to use modals, and it uses a flyout modal that opens from the right side. This is because the button that triggers the modal is also on the right side, so you have less mouse movement from the button that triggered the modal to actually fill the form. Hurrah!

Then I added breadcrumbs to all the pages. How hasn’t one lost in deep navigation and not actually knowing how to go back to a previous page? I have had that feeling several times on most web apps. Well, breadcrumbs are quite handy to know exactly the current navigation, so you can be deep on the page that shows all the deployments for your app and still go back to the server page for the site with one click.

Next, I added UI copy for all pages. Some pages mostly don’t need too much text; however, it’s nice to have a little reminder of what the current page is about. Also for forms, so you can actually be sure you are on the correct form by reading the heading and description. And since I’m already adding text, I have added descriptions to all fields, so it clearly states what the field is about and how it is expected to be filled. Fewer or no error forms when hitting the submit button.

Finally, I added icons for the server and SSH keys navigation links on the sidebar, just as a visual aid and for easy scanning.

Lastly, okay, the previous one was not the final. I added a clarification that to provision a server with Fuse, the server should be provisioned with your server provider with the latest Ubuntu LTS version. There are a lot of Linux flavors, but to keep this simpler, I chose to only support Ubuntu and the LTS version so you can be sure that the server you have provisioned will have years to come to receive security fixes. Your server will last longer.

That’s it for now. Keep shipping and give Fuse a try.