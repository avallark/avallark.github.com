---
layout: post
title: iPads & Tablets to enrich in-class learning experience
---
# iPads & Tablets to enrich in-class learning experience

I was in charge of the IESE iPad application that was made to enable distribution of materials, class session slides etc. and enabling them to read and annotate on them. They could potentially share notes and annotations with other classmates. To enable further team work, we decided to use further collaboration tools, that could keep teammates in touch with each other wherever they are.

This was the first application made in this space to be really used in class. [The coverage, we got in FT is here](http://www.ft.com/intl/cms/s/2/c9844f52-35fd-11e0-9b3b-00144feabdc0.html#axzz1gO9YEJ5x)

## Why am I writing this post?
Being one of the first pilots in this domain of using Tablets in education, there were several difficulties. Hopefully our experience that is documented here would be of help for others who are trying to use these tablets in classes. Feel free to [get in touch with me](mailto:bijur@grep-i.com) if you need my help or guidance in this aspect.

## Provider
#### Selection of Vendors & Lack of experience
Most vendors in this area are small scale. The larger consulting companies have not started making mobile application development a part of their business. Thus typical suppliers of this service are small companies with limited resources, experience and capabilities.

We opted a model of having annotation libraries from iAnnotate and a simple UI integrated with these libraries for the distribution of content.

On hindsight, and with better experience on portals like [elance](http://elance.com), I would highly recommend building a  n application using a vendor on Elance following a scrum methodology.

## Back Office

The level of unpreparedness within the organization to distribute content digitally was startingly surprising to us. Our processes were extremely streamlined to print materials, but was hugely inconvenient when it came to using the digital version of the same content.Some of the difficulties were with case formats, copyrights, distribution servers, security etc.

#### Case formats

We had to debate on the format of the materials. These materials are typically cases and technical notes that forms the core part of our business as a school. Thus we had an infrastructure built around DRM. The digital rights to distribute cases in the electronic format was unavailable and students were allowed to have only paper based cases.
We analysed .mobi, .epub and pdf as the possible solutions. Creating annotations over the .mobi and .epub formats were the easiest as they were a lot more interactive, but building new libraries from scratch was a daunting task and our supplier was not capable of this. Thus we decided to use pdf as our delivery method. This also helped us to avoid having to convert the already existing pdfs to other formats.
#### Copyrights of Materials

The pdfs have to have the following conditions as per current agreements with other publishing vendors:

* Social watermark on the sides saying these contents are distributed to students for a particular course and program

* The files should be distributed through an IESE only intranet/medium

* Limit the number of iPads that can actually install the applications. We did this using the provisioning certificate from the Apple Enterprise account of the school. So unless we enable the particular udid number in our enterprise account, the ipad will not be able to install this application. 

As you can imagine some of these restrictions made scalability a very difficult task for us. Since then we have made some improvements in processes and in the way the Application is installed so as to overcome these scalability bottlenecks.

#### Automatic distribution of content

The content has to be automatically available to students instead of student having to download the materials one by one. This involved a huge effort as this required integrations with the course calendar, a server delivering content with 100% uptime and enough storage on the device to store all content, to be able to work offline. The devices also had to be connected with 3G or mobile data as well.

## IT - Project & Support

Dealing with the change management in IT itself is huge step. considering we have an ageing IT with old skillsets training them in new technologies was very important task.

#### New technology & Project Methodology

For IT this is a disruptive change. The technology is new, the skillset is new. The traditional models of managing information is not enough. 

Most new suppliers deal with Agile methodology using SCRUM to manage projects. Traditional waterfall methodology is what IT is used to and new methodology takes getting used to & more importantly to get accepted.

Scrum methodology though unsettling for first time users (our CIO and Project Management Office being two of them) has great advantages to counter and reduce risks. The time to market for a product also reduces greatly. Giving us the opportunity to be out with a product in 3 months and then progressively adding more and more features.

I will elaborate on the scrum methodology we used to get this project done later. 

#### Traditional Support

The traditional support provides support 08:00 to 19:00 from Monday to Friday.  Without the paper based cases, students when they study need to be able to use the iPads and the applications. The problem is that students in our executive programs study after they get home from work, which is usually after 20:00. Thus support should be available to them after this time. 
This was impossible for our support organization.

#### Collaborative Support through Socialcast

[Socialcast](http://socialcast.com) is a twitter like microblogging platform where all the employees of a company share debates, work updates and issues. 

We used this platform in a way such that whenever a student faced an issue, we encouraged them to post to socialcast which meant that it got not only our responses, but also responses from other student. This transparent form of support ensured that common issues are resolved fairly fast, even sometimes with IT getting involved.


