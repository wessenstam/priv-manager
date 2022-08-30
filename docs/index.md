# Before You Begin

## Purpose

This training and lab guide is designed to accompany a Delinea trainer lead course. During your training course the trainer will regularly reference this guide as well as demonstrating lab exercises within a shared desktop environment and discussing common use cases and real-world scenarios.

## Your training pack

Before you start this training course, ensure you have received lab details from your Delinea trainer.
The Secret Server lab consists of the following machines:

| Machine Name | Internal Lab Name | Description |
|--------------|-------------------|-------------|
|DC1|DC1|Domain Controller - contains all AD configuration used within the lab|
|SSPM|SSPM|This machine will be used to install and host Privilege Manager|
|Client|Client01|Windows server, used to test a range of Privilege Manager functionalities during the training course|

All lab machines can be accessed easily from the Skytap URL provided by your trainer.

The administrative credentials you will need to log into the lab machines:

**Windows Domain Admin Account**

  * Username: thylab\\adm-training
  * Password: *Password will be provided by trainer*

**Windows Domain Standard User Account (for testing policy)**

* Username: thylab\\StandardUser
* Password: *Password will be provided by trainer*

## Introduction

Your trainer will provide a slide-based introduction to Privilege Manager, the slide deck used will
be shared.

## General remark

When logging into the Client01 VM as "normal" none administrative account, please be patient as due to new updates of Windows that have been installed, lots needs to be updated in the backend... It may take 1-3 minutes per user. Also the first time you open the Privilege Manager UI it will take time to get IIS ready to serve the UI. This is only on the first time the UI is opened.
