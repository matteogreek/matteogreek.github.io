---
title: OhSINT
summary: Open Source Intelligence simple task
tags:
  - writeup
date: "2023-08-04"

# Optional external URL for project (replaces project detail page).
external_link: ''

reading_time: false  # Show estimated reading time?
share: false  # Show social sharing links?
profile: false  # Show author profile?
comments: false  # Show comments?
---
## Task1

> What information can you possible get with just one photo?

### Question 1
What profile picture does this user have?

Let's start by downloading the task files. We can see that the file attached to this room is an image called *WindowsXP.jpg*. Let's run **exiftool** to analyze the metadata of the file and see if we can find some useful information.

By looking at the result, under the copyright data we can take note of a what it seems a username (OWoodflint). 
Since the goal of the room is learn what is OSINT we have to proceed and search on the web the username we just found to obtain publicly available information about the target. 

There are many ways to do it, one is by using **sherlock** or other OSINT tools that automate the process of finding usernames across many social networks. 

To perform the actual search we can type the following command where *–timeout* is the time (in seconds) to wait for response to requests. A longer timeout will increase the likelihood of getting results from slow sites but on the other hand, this may result in a long delay in gathering all the results. 

> python3 sherlock.py OWoodflint –timeout 15

There are multiple accounts with that username registered on various websites, some
of which may not belong to the individual we are looking for. Let’s start by looking at the twitter account. By opening the target’s profile we can answer what the profile picture this account has.

<details>
  <summary>Answer:</summary>
  <p>
	cat
  </p>
</details>


### Question 2
> What city is this person in?

Looking at the target’s profile we can observe that one tweet contains the BSSID of one of his neighbors.
The BSSID or Basic Service Set Identifier is a unique 48-bit label associated with an individual access point. With this information we can use **Wigle.net** which is a website that collects location and other data from wireless networks worldwide. Volunteers gather this data by downloading an app to their phones, which registers all APs they meet as well as their GPS coordinates. All of this information is then uploaded into the database. This data is then displayed to viewers on the website.
Let’s try to locate our target. Navigate to Wigle.net and enter the BSSID found on twitter. The result is an address where the city is the answer.

<details>
  <summary>Answer:</summary>
  <p>
	London
  </p>
</details>

### Question 3
> Whats the SSID of the WAP he connected to?

To answer just look at the result we obtained on Wigle.net for the previous question. In addition to the location there is also the SSID we are looking for. 

<details>
  <summary>Answer:</summary>
  <p>
	UnileverWiFi
  </p>
</details>

### Question 4
> What is his personal email address?

We have to search on other websites to answer this.  Let's open the github account related to the same username. We can see a public repository called *people_finder*.  On the README.md file there is the email address. 

<details>
  <summary>Answer:</summary>
  <p>
	OWoodflint@gmail.com
  </p>
</details>

### Question 5
> What site did you find his email address on?

The name of the site where we found the email address.

<details>
  <summary>Answer:</summary>
  <p>
	Github
  </p>
</details>

### Question 6
> Where has he gone on holiday?

By googling OWoodflint there is a wordpress website where we can find more information. On the mainpage of the blog there is a post where the author says where he is right now.

<details>
  <summary>Answer:</summary>
  <p>
	New York
  </p>
</details>

### Question 7
> What is this persons password?

To answer this we need to view the source code of the websites. Looking at the code we can try and search for keywords like 'psw', 'password' or similar but nothing pops out. looking at the body of the page we can notice a paragraph with the color set to white where the text is a strange string which is the final answer.

<details>
  <summary>Answer:</summary>
  <p>
	pennYDr0pper.!
  </p>
</details>


**Hurray!**

[Heartstone back home](https://matteogreek.github.io/)