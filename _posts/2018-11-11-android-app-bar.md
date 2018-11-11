---
layout: post
title: "Android App Bar"
description: "Native ActionBar vs. Toolbar"
date: 2018-11-11
---

Implementing of Action Bars is a little bit confusing because you have to distinct between native
ActionBars and the newer support library's toolbar. In short you should use the toolbar as the native
action bar behaves differently depending on the Android version.

To disable the native action bar and to use the support library's toolbar you have to use one of 
appcompat's NoActionBar themes, like <code>Theme.AppCompat.Light.NoActionBar</code>.
