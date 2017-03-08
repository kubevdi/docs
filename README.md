# KubeVDI Documentation

This repository is for general purpose documentation and architectural discussions / documents and images.

At the moment it has one big section: talk about the prototype, lessons learned, and how to do it better.

## Prototype

There is already a version v0.1.0 out there which is working and provides remote desktops to end users. However, the goal of this prototype was different and should be outlined here.

**NOTE:** the source code of v0.1.0 is not available as this work cannot be open sourced due to company policies. This is one of the reasons why we need to start from scratch again (and it is probably a good idea).

### Prototype Architecture
The architecture of it can be best described in a picture like this:

![prototype architecture][prototype-architecture]

### Prototype User Experience

In the prototype you basically had two options on how to connect: with the `kubevdi-client` or with a normal browser window.

We are going to walk through the user experience in this section assuming that we are using the `kubevdiclient`.

Once you open the `kubevdiclient` which is an Electron App and basically just a special browser window which takes care that certain headers are always set which a browser does not do on its own, you will see the login page _if you have not logged in before_.

![prototype kubevdi login][prototype-kubevdi-login]

You are redirected to do the well-known OAuth procedure:

![prototype oauth 1][prototype-kubevdi-oauth-1]
![prototype oauth 2][prototype-kubevdi-oauth-2]
![prototype oauth 3][prototype-kubevdi-oauth-3]

Now every 15min (or actually this is a configurable value) you are required to do an additional 2FA. It is basically done on every new request (it is implemented as a middleware).

![prototype 2fa][prototype-kubevdi-duo-2fa]

Once you have (finally) completed, you are presented with your _session list_ window. Here you can see, connect and delete your sessions, as well as create new ones.

![prototype session list][prototype-kubevdi-session-list]

From the session list view, you can reach your final session - which is a kubernetes pod running a desktop for you. In this example here, it is a really slim non-user-friendly _twm_ running Firefox.

![prototype session view][prototype-kubevdi-session-running-firefox]

### Prototype Goals

The goals of this prototype were extremely specific because they had to suit our particular use-case at the time - which is a bastion host (jump host) with additional requirements:
- secure access into a kubernetes cluster
- 2FA and audit logs
- **no copy&paste** to prevent data exfiltration
- no possible data-streams (like SSH connections) that easily allow for data exfiltration
- no remote-mountable filestorage to prevent data exfiltration
- in summary: a remote-control application with strong security and no data exfiltration possibilities

### Lessons Learned

TODO

[prototype-architecture]: https://raw.githubusercontent.com/kubevdi/docs/master/images/prototype-architecture.png "Prototype Architecture"
[prototype-kubevdi-login]: https://raw.githubusercontent.com/kubevdi/docs/master/images/prototype-kubevdi-login.png "Prototype Login Page"
[prototype-kubevdi-oauth-1]: https://raw.githubusercontent.com/kubevdi/docs/master/images/prototype-kubevdi-oauth-1.png "Prototype OAuth Step 1"
[prototype-kubevdi-oauth-2]: https://raw.githubusercontent.com/kubevdi/docs/master/images/prototype-kubevdi-oauth-2.png "Prototype OAuth Step 2"
[prototype-kubevdi-oauth-3]: https://raw.githubusercontent.com/kubevdi/docs/master/images/prototype-kubevdi-oauth-3.png "Prototype OAuth Step 3"
[prototype-kubevdi-duo-2fa]: https://raw.githubusercontent.com/kubevdi/docs/master/images/prototype-kubevdi-duo-2fa.png "Prototype Duo 2FA"
[prototype-kubevdi-session-list]: https://raw.githubusercontent.com/kubevdi/docs/master/images/prototype-kubevdi-session-list.png "Prototype Session List"
[prototype-kubevdi-session-running-firefox]: https://raw.githubusercontent.com/kubevdi/docs/master/images/prototype-kubevdi-session-running-firefox.png "Prototype Session running Firefox"
