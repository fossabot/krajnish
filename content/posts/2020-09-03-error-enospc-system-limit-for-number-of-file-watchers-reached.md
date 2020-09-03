---
template: post
title: "Error: ENOSPC: System limit for number of file watchers reached"
slug: error-enospc-system-limit-for-number-of-file-watchers-reached
draft: false
date: 2020-09-03T11:55:25.373Z
description: "Resolve the Error: ENOSPC: System limit for number of file
  watchers reached while running NPM or Gatsby"
category: NPM
tags:
  - NPM
  - Gatsby
---
![Error: ENOSPC: System limit](/media/system-limit-eeror-node.jpg "Error: ENOSPC: System limit")

If you are getting error as above while running NPM or Gatsby then you need to increase the `max_user_watches` by running the below command. 

View the current limit by running:

```shell
cat /proc/sys/fs/inotify/max_user_watches
```

Increase the limit to its maximum by editing ```/etc/sysctl.conf` `` and adding this line to the end of the file:

```shell
fs.inotify.max_user_watches=524288
```

Load the new value by running `sudo sysctl -p`.
Now your NPM or Gatsby commands run without any error.

![resolve-ENOSPC: System limit ](/media/resolve-max_user-error-npm.jpg "resolve-ENOSPC: System limit ")