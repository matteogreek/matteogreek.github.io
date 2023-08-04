---
title: Mr. Phisher
summary: Phishing email containing suspicious attachment


# Optional external URL for project (replaces project detail page).
external_link: ''

reading_time: false  # Show estimated reading time?
share: false  # Show social sharing links?
profile: false  # Show author profile?
comments: false  # Show comments?
---
## Task1
Deploy the machine attached to the room to access the files. 
### Question 1
> Uncover the flag in the email attachment!

The task of the room says that the document attached to a suspicious email keeps asking to enable macros.
We can use this information as a guide for starting the research of the flag. We can deduce that some kind of useful information is related to the document's macros.

First of all let's open the file called *MrPhisher.docm* with LibreOffice. Then to see what macros are set for the document go to *Tools > Macros > Edit Macros*.
Under *Modules* we can see *NewMacro*, if we open it we see the macro related of MrPhisher.doc.

![macro](https://user-images.githubusercontent.com/70201797/180665401-31f055cb-5f80-4056-a9d9-a3e45ce1e1a9.png)

We can note that it's a macro written in Visual Basic. For simplicity we can easily convert the code to python.

![code1](https://user-images.githubusercontent.com/70201797/180665413-6ece7625-e923-4fdf-8515-eec88e8c4e44.png)

The code is straightforward, each element of the array is xor-ed with the relative index of that element. The result is casted to char to form the final output. 

Let's run it and see what the result is. Oh wait it's the flag!

<details>
  <summary>Answer:</summary>
  <p>
	flag{a39a07a239aacd40c948d852a5c9f8d1}
  </p>
</details>


**Hurray!**

[Heartstone back home](https://matteogreek.github.io/)
