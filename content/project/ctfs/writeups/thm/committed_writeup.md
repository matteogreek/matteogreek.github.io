# Committed
## Task1

Some sensitive code was leaked and committed to a GitHub repository. The goal is to find what was committed.

### Question 1
> Discover the flag in the repository!

Start by deploying the machine attached to the room to access the the files we need. Inside the machine we find *committed.zip*. 

We know that we need to find some leaked information on some accidental commit. To know all the past commit to a git repository we can type:

> git log --reflog

where reflog is a record of all commits that were referenced in the repo at any time.

![Screenshot_2022-07-23_16-06-10](https://user-images.githubusercontent.com/70201797/180622496-e3981949-7483-40ec-a1a2-27152d6d2b97.png)

Looking through the results one commit stand out with the message text set as *Oops*. To show the content of the commit we can use the command:

> git show \<hash\>

where \<hash\> is the hash of the commit that we want to show. It's easy now to find the string with the flag.

<details>
  <summary>Answer:</summary>
  <p>
	flag{a489a9dbf8eb9d37c6e0cc1a92cda17b}
  </p>
</details>



**Hurray!**

[Heartstone back home](https://matteogreek.github.io/)