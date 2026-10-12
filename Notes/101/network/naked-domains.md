---
# Mandatory fields
id: "6a9f4803-9502-4199-b8b5-c7f00fb8466d"
# Optional fields
title: "What is a naked domain"
tags: []
source: "https://help.pythonanywhere.com/pages/NakedDomains/"
source_title: "Naked domains | PythonAnywhere help"
source_description: "What is a naked domain? When you buy a domain name from a registrar, you become the owner of something like yourdomain.com.  What this means is that you can create entries in the Domain Name System th"
source_image_url: ""
created_date: "15-09-2023"
modified_date: "23-09-2023"
---
When you buy a domain name from a registrar, you become the owner of something like yourdomain.com. What this means is that you can create entries in the Domain Name System that end with yourdomain.com, like www.yourdomain.com, api.yourdomain.com, ftp.yourdomain.com, and so on. In a strict technical sense, these are also domain names, and the term "naked domain" -- sometimes also called an "apex domain" -- has been coined to refer to the bit of the domain name you originally bought -- just the yourdomain.com without anything in front of it.

It's important to know that all of the above are completely different domain names in a technical sense. You could in theory have one website on yourdomain.com, another different one on www.yourdomain.com, another on somethingelse.yourdomain.com, and so on.

What that means is that if you set up a website at www.yourdomain.com on PythonAnywhere, people will be able to view it if they enter that exact name into their browser. If they just enter yourdomain.com then they will get something else -- exactly what they see will depend on how your DNS settings are configured. Likewise if you managed to set up a website for yourdomain.com, it would not show up if people typed in www.yourdomain.com.

So for a website, you generally want people to be able to visit it by typing in either of the normal versions of the address -- the one with the www. at the start, or the one without. If you put your website on just one of them, some people will use the other one and get confused when they don't see anything.

The recommended is that you have the "official" version of your website on www.yourdomain.com, and then set things up so that yourdomain.com automatically redirects people to that official version. The rest of this page explains how to do that last step.

Or you can just have two separate copies of your website, one at yourdomain.com and one at www.yourdomain.com.