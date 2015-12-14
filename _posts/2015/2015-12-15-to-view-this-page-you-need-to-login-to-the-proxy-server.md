---
layout:     post
title:      To view this page, you need to login to the proxy server.
date:       2015-12-15
summary:    Stuck behind a NTLM based proxy server in a windows only corporate environment on a MacBook? Here's how you can make the best out of bad situation.
categories: xamarin corporate soe ntlm proxy internet cntlm
---

If you have ever been in the unfortunate situation whereby you are using a Macbook/OSX device within a Windows centric environment and are forced to use a proxy server then the words above and the image below will potentially send shivers down your spine.

![To view this page, you need to login to the proxy server.](/images/osx-ntlm-proxy-auth.png)

What's the big deal you ask? Surely it's just a matter of entering in your username (```domain\username```) and password. Two minutes later (if your lucky) that damn prompt will come back regardless if you selected "Remember this password in my Keychain" and clicking "Cancel" is about the worst possible thing you can do.....

![To view this page, you need to login to the proxy server.](/images/osx-ntlm-proxy-auth-loop.png) 

Luckily, thanks to the magic powers of open-source software there's a solution!

    # brew install cntlm

Next step is to generate a encrypted NTLMv2 hash which will be used instead storing your password in plain text.

    # <wip>

Edit the configuration file at ```/usr/local/etc/cntlm.conf```:

    <wip>

Replace `$username`, `$ntlmHash` and `$domain` as needed and add any proxy exceptions to ```WIP```

Configure `cntlm` to launch automatically:

    # <wip>

Configure OSX to use the proxy server that is now running at ```localhost:3128```

In 31 days or whenever you windows password chasnges/expires you will need to re-run the `$ntlmHash` command, update the configuration file with the resulting output and restart the daemon.

