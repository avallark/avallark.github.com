---
layout: post
title: NCERT Textbooks in a download friendly format.
author: Abdul Bijur Vallarkodath
---

# NCERT Textbooks in a download friendly format.

First things first, the [Project is available on Github](https://github.com/avallark/NCERT-TextBooks).

A friend of mine was preparing for the UPSC services examination and he asked my help to locate the NCERT textbooks as that is a good place to start preparing. I found the NCERT website quite fast, but found out that downloading these files from the website is a pain. They make each chapter a separate pdf and cover pages jpg formats. All in all you have to download 20 files if you want to read a text book.

Thus, I started a project so as to unify these pdf files into a single more human-form pdf. The pdf would thus be a complete ebook for one subject of NCERT. To do this, I needed three things

* a tool to download these files easily : wget
* a tool to combine these pdfs into a single file : gs (ghostscript)
* a tool to convert jpg to pdfs : ghostscript/ImageMagik

All these tools are free open source tools that can be used. So I created two scripts jpg2pdf and compdf to ease their usage.

*compdf* takes in two arguments, 1st is the final pdf name e.g. 8th-Maths.pdf, and the second is the list of pdf file to be merged. The order that is given here is important.

usage:
        compdf "Final pdf name" "coverpage.pdf hesc10?.pdf hesc11?.pdf hesc1an.pdf"
e.g. 
        compdf "9th-Science-Problems.pdf" "ieep1cc.pdf ieep1ps.pdf ieep10?.pdf ieep11?.pdf ieep1a?.pdf"

*jpg2pdf* is required as compdf can only merge pdfs and some coverpages are given in jpg files. so you will need to convert them to pdf.

usage:
        jpg2pdf JPEG-Filename.jpg PDF-Filename.pdf 


_Note, most probably the jpg2pdf will error out on your computer because of the location of the viewjpeg.ps file on your computer. It will be different on your computer so use locate or find to find this file and then replace the path to that file in the jpg2pdf script._

These both tools are also added in the scripts folder of the project.

I used these tools and have uploaded a few textbooks, mostly those relevant to the UPSC civil services examinations.So folks who are preparing for it, can download the complete textbooks from this website.

## Plea to contribute

While I was creating this, I realised that this is a good way of trying to provide a way for people to easily download pdf files directly to their computers, without having to worry about merging the pdfs etc. I have provided you with all the tools you will need, in the scripts folder.

If you have some time, rather than wasting it on tv, [make yourself interesting](http://www.forbes.com/sites/jessicahagy/2011/11/30/how-to-be-interesting/) use it to contribute to this project. Your efforts would be greatly appreciated by the millions of kids in India who will be helped by this deed of yours.


If you have unmerged pdf files, you can also contribute by uploading them to the directory called "unmerged". I will merge them as soon as I can.

#### A note about copyrights
All copyright belongs to NCERT. I only function as a facilitator and do not own any copyright. We thank NCERT for making these textbooks available in the public domain.

