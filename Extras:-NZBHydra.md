

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:0 orderedList:1 -->

1. [Introduction](#1-introduction)
2. [URL](#2-url)
3. [Initial Setup](#3-initial-setup)
	1. [Domain](#i-domain)
	2. [Install](#ii-install)
4. [Settings](#4-settings)
	1. [Authorization](#i-authorization)
	2. [Indexers](#ii-indexers)
	3. [Downloaders](#iii-downloaders)
5. [Sonarr](#5-sonarr)
6. [Radarr](#6-radarr)
7. [API](#7-api-key)

<!-- /TOC -->

## 1. Introduction


[NZBHydra v1](https://github.com/theotherp/nzbhydra) (by TheOtherP) is a meta search tool for NZB indexers. It provides easy access to a number of NZB indexers. You can search all your indexers from one place and use it as indexer source for tools like Sonarr or CouchPotato.


![](https://i.imgur.com/FZnV0Ru.png)

---

_Note: By default, Cloudbox will install NZBHydra2, as NZBHydra v1 is no longer being developed. But it is available to users who still want to use it._

---

Three Ways to setup NZB indexers with Sonarr/Radarr/Lidarr: 

1) Skip this page and add all your NZB Indexers directly into Sonarr/Radarr/Lidarr. Benefit from the seeing indexer sources during manual lookups in Sonarr/Radarr/Lidarr. This method is also useful when diagnosing issues with indexers during failed searches;

2) Add all your NZB Indexers directly into Sonarr/Radarr/Lidarr, but also add them in NZBHydra2, so it could be used a tool for manual downloads; or

3) Add all your NZB indexers in NZBHydra2 and then just add the one NZBHydra2 "indexer" into Sonarr/Radarr/Lidarr. This is the most popular choice among users.


---



## 2. URL

- To access NZBHydra: https://nzbhydra._yourdomain.com_


## 3. Initial Setup

### i. Domain

See [[Adding a Subdomain|Adding a Subdomain]] on how to add the subdomain `nzbhydra` to your DNS provider.

_Note: You can skip this step if you are using [[Cloudflare|Prerequisites: Cloudflare]] with Cloudbox._

### ii. Install

Run the following commands:

 ```bash
 cd ~/cloudbox/
 sudo ansible-playbook cloudbox.yml --tags nzbhydra
 ```

## 4. Settings

Enter setup by clicking on "Config" at the top.

### i. Authorization

1. Change "Auth type" to `Login form`.

1. Set all the options below to `ON`.

1. Click "Add new user".

1. Fill in your username and password.

1. Click "Save" (top right).

 ![](https://i.imgur.com/IAxSk4P.png)

### ii. Indexers

- Add your indexers. Be sure to click "Save" when done.

### iii. Downloaders

1. "Add new downloader" -> "NZBGet".

1. Fill in the following:

   - Name: NZBGet

   - Host: `nzbget`
   - Port: `6789`
   - Use SSL: `OFF`
   - Username: [[Your NZBGet Username|Install: NZBGet]]
   - Password: [[Your NZBGet Password|Install: NZBGet]]
   - Default category: _Leave Blank_ (`No category` doesn't work too well)
   - NZB access type: `Redirect to indexer`
   - NZB adding type: `Upload NZB` (works better than `Send link`)

   ![](https://i.imgur.com/n3ZV0Ki.png)




## 5. Sonarr



1. Open Sonarr: https://sonarr._yourdomain.com_

1. Go to "Settings" -> "Indexers".

1. Click Add Indexer (`+`).

1. Select "Newznab".

1. Add the following:

   1. Name: NZBHydra

   1. Enable RSS Sync: _Your Preference_

   1. Enable Search: _Your Preference_

   1. URL: `http://nzbhydra:5075`

   1. API Key: [[Your NZBHydra API Key|Extras: NZBHydra#7-api-key]].

   1. Additional Parameters: _Leave Blank_

1. Your settings will look like this:

    ![Sonarr NZBHydra2](https://i.imgur.com/lQeKy7w.png)

1. Click "Save" to add NZBHydra.

Note: The "Test" will keep failing until you add an indexer in NZBHydra.


## 6. Radarr


1. Open Radarr: https://radarr._yourdomain.com_

1. Go to "Settings" -> "Indexers".

1. Click Add Indexer (`+`).

1. Select "Newznab".

1. Add the following:

   1. Name: NZBHydra

   1. Enable RSS Sync: _Your Preference_

   1. Enable Search: _Your Preference_

   1. URL: `http://nzbhydra:5075`

   1. API Key: [[Your NZBHydra API Key|Extras: NZBHydra#7-api-key]].

   1. Additional Parameters: _Leave Blank_

1. Your settings will look like this:

    ![Radarr NZBHydra](https://i.imgur.com/ZWYqzCS.png)

1. Click "Save" to add NZBHydra.

Note: The "Test" will keep failing until you add an indexer in NZBHydra.


## 7. API Key

To find the NZBHydra API Key, go to "Config" --> "Main". This will be used later.

