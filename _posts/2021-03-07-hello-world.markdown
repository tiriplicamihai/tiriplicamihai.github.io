---
layout: post
title:  "Hello World!"
date:   2021-03-07 19:30:20 +0200
categories:
---

As per Software Engineering customs, my first post is "Hello World!". I decided to start this blog after reading Chad Fowler's [	
The Passionate Programmer](https://pragprog.com/titles/cfcar2/the-passionate-programmer-2nd-edition/). One of the best (and most recurrent) advices about learning is to teach what you want to learn. My plan for this blog is to teach myself how to write and, at the same time, share my adventures in Softwareland.

To get a meta flavor, we'll continue to how this blog is built.

## Building a blog

I had this on my mind for a long time, I thought about different complicated ways of building it, from writing my own blog management tool to using Terraform to deploy it on AWS and to use lambdas as a backend. As you've probably already guessed this never happened and mostly because of two reasons - **the amount of work seemed overwhelming** and **I did not know what I wanted**.

The funny part is that I am an Agile and simplicity advocate and I was completely ignoring my work principles. Taking a few steps back, I still don't know what I want but I plan to find out by taking small steps in whatever direction I find interesting at that moment so I just defined a set of requirements for an MVP:

1. Focus on content rather than tooling
1. Own my content (this excludes some blogging platforms)
1. Flexibility (more like, I want to be able to build custom things for the sake of learning)
1. Cheap (as in free)
1. Activity tracking
1. Custom domain name

For these I explored 2 options.

### AWS S3 Website Hosting

I do have a bit of experience in AWS and knew that it's possible to upload a static website to S3 and serve it via Cloudfront. You can find the documentation [here](https://aws.amazon.com/premiumsupport/knowledge-center/cloudfront-serve-static-website/) but the gist of it is

1. Create an S3 bucket
1. Configure HTTPS
1. Upload your site to the bucket
1. Configure DNS and Cloudfront 
1. Upload your code

Besides the steps above I will also need a Github repo and a minimal script to build and deploy the site (probably a bash script using AWS CLI). Not that bad considering that you can get SSL certificates from AWS and also get a domain name. Neat!

Now, I want to focus on my content, I don't have a lot of frontend experience, my plan is to get it and share it on this blog so chicken and egg problem. Googling for solutions got me to [Jekyll](https://jekyllrb.com/) which is awesome and dummy proof enough that I can use it. I go down the rabbit whole and find [Jekyll Themes](https://jekyll-themes.com/) which help with another gap in my plan - user experience. And what's even great a lot of them are open source, I can use them, make changes if I need to and if I get good at this I can create my own.

Following the Jekyll documentation I found an interesting idea - it works great with Github Pages. Remember how I said I have to create a Github repo besides the AWS account? How nice would it be to need one thing instead of two? Besides, I plan to have a lot of success (LOL) and AWS will start charging if the traffic blows up. So here comes my second option.

### Github Pages

Spoiler alert: this is the winner!

Jekyll and Github Pages are a match made in heaven. I use a single tool, there are no charges for now and I don't have to work on my deploy script either. Github provides a [guide](https://docs.github.com/en/github/working-with-github-pages/setting-up-a-github-pages-site-with-jekyll) to get you started and I can tell it took me around half an hour (including installing redis and jekyll) on top of the half hour deciding on a theme.

Remember how I told you I like simplifying things? Looking at my MVP I realized that I don't really need a custom domain name for now, I can get feedback on my content and validate my ideas with the Github Pages domain. Github has a nice [guide](https://docs.github.com/en/github/working-with-github-pages/configuring-a-custom-domain-for-your-github-pages-site) to this and I think I'll do it sooner rather than later and write about the experience.


Hopefully this will be useful for other people as well. If you have any feedback to reach out either on social media or Github!