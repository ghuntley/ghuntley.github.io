---
layout:     post
title:      Xamarin In A Corporate Environment
date:       2015-12-14
summary:    Stuck doing Xamarin development in a windows only corporate environment on a MacBook? Here's how you can make the best out of a bad situation.
categories: xamarin corporate soe virtual-machine windows visual-studio xamarin-studio vmware-workstation
---

When working in a corporate environment I usually have my Macbook Pro setup as follows:


	+--------------------+    USB PASS-THROUGH INTO VIRTUAL MACHINE
	|                    | <------------------------------------------+
	|                    |    WHEN DOING UWP DEVELOPMENT              |
	|                    |                                            |
	|   VIRTUAL MACHINE  |                                            |
	|                    |                                            |
	|                    |           MACBOOK PRO LAPTOP               |
	|                    | +-----------------------------------+      |
	|                    | |                                   |      |
	|                    | |                                   |      |
	|   CORPORATE SOE    | |                                   |      |
	|   WINDOWS 7/8/10   | |              MAC OSX              | +----+---+
	|   VISUAL STUDIO    | |          XAMARIN STUDIO           | |        |
	|                    | |                                   | |        |
	|    UWP UI & PCL    | |        IOS UI & ANDROID UI        | |        |
	|                    | |                                   | |        |
	|                    | |                                   | | MOBILE |
	|                    | |                                   |<+        |
	|                    | |                                   | |        |
	|                    | |                                   | |        |
	|                    | |                                   | |        |
	|                    | |                                   | |        |
	+---------^----------+ +--------------------^--------------+ +---^----+
	          |                                 |                    |
	+---------+----------+ +--------------------+--------------------+----+
	|    CORP NETWORK    | |              DIRECT INTERNET                 |
	|  USB ETH ADAPTER   | |           INBUILT WIFI ADAPTER(s)            |
	+--------------------+ +----------------------------------------------+

By using an Apple USB Network Adapter ([which does work on Windows](/archive/2015/12/14/apple-usb-network-drivers-for-windows/)) and using the USB pass-through feature of VMWare Workstation it is possible for a single machine to be connected to two different networks without voilating your IT security policy. 

When I need direct internet access on the virtual machine then that is achieved by disconnecting the adapter and temporarily changing the virtual network adapter mode from host to bridged/nat. 

This setup allows the best of both worlds, simultaneous direct internet access and access to corporate resources such as bug trackers, source control, email, intranet and timesheet systems.

I find some form of direct internet connectivity is an absolute must when doing mobile development otherwise productivty tends to go out the window. If you are in the unfortunate circumstance whereby you have to use a Windows NTLM based authentication proxy server on Mac OSX then I suggest reading [this article for a solution](/archive/2015/12/15/to-view-this-page-you-need-to-login-to-the-proxy-server/). 
