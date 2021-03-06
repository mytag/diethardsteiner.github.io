---
layout: post
title: "Pentaho Data Integration: Restartable Job"
summary: This article explains how to easily add restartablility to Pentaho jobs
date: 2017-07-21
categories: PDI
tags: PDI
published: true
---  


This blog post could as well be labeled *The world's simplest restartable job*. My main aim here is to have a fast and easy implementation, without any dependencies. It is very simple and very basic. 

The idea is that we create an empty file (a **control file**) for every **unit of work** successfully done. Simple. That's it really. If a unit of work does not get completed successfully, no file will be written out. Before executing a unit of work, we check if the **control file** exits. If it exists, we do not execute the current unit of work, but move on to check if the **control file** for the next unit of work exists. Once we completed the last unit of work successfully, we know that the whole **process** finished successfully, hence we can **delete** all **control files.**

> **Note**: With this setup you can only execute units of work sequentially and care must be taken within your units of work that everything is really restartable.

> **Note**: When you take a look at the screenshot of the Pentaho Data Integration job, you will notice that the unit of work is represented by a *Wait* job entry. In reality, this would be a job or transformation job entry.

![](/images/pdi-restartable-jb-1.png)

