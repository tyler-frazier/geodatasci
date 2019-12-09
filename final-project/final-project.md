---
description: >-
  Create a GitHub Pages site and populate it with the results from your
  geospatial data science investigation on your selected LMIC and administrative
  subdivision(s).
---

# Final Project

For the final project in this course you will create a **GitHub Pages** site using a fairly simple programming language called markdown and populate that site with content you have created through the course of this semester.  Upon completing your GitHub Pages site, post a link to your website on the slack channel \#data100\_final prior to the deadline of 5PM on Wednesday, December 18th.

To begin go to [https://github.com](https://github.com) and create a new account.  You should see a website that is very similar to the following image.

![](../.gitbook/assets/screen-shot-2019-12-08-at-9.15.32-pm.png)

After clicking on the sign up link, create your account by designating your username, e-mail address and password.  In order to simulate the process of signing up, I am using the username `wicked-problems.`  My real GitHub account is [https://github.com/tyler-frazier](https://github.com/tyler-frazier), and you are welcome to follow me, although it is not necessary for this final project.

![](../.gitbook/assets/screen-shot-2019-12-08-at-9.08.29-pm.png)

![](../.gitbook/assets/screen-shot-2019-12-08-at-9.11.13-pm.png)

After creating your account, you should receive an e-mail asking to verify your account.  Go ahead and verify, so GitHub can permit you to create a new repository.  Once you verify your e-mail address, GitHub will likely ask if you want to create a new repository.  If somehow you are not automatically asked to create a new repository, it is also possible by selecting the + pull down arrow in the top right corner of the page.

![](../.gitbook/assets/screen-shot-2019-12-08-at-9.28.39-pm.png)

You will also notice that there is a guide made available for new users \(the green, read the guide tab\).  This is really good guide to read, in order to learn how to use GitHub as a version control system.  Although you will be using only a small amount of GitHub's full potential for this final project, I highly recommend making a mental note of the guide and returning to the 10 minute read when you have some time.  If you are planning to major or minor in Data Science, Computer Science, or any discipline that has a signficiant compuational component, it will be very likely that at some point in the future you will need to use a version control system \(such as GitHub\) for repository control, sharing, collaboration, conflict resolution etc...[https://guides.github.com/activities/hello-world/](https://guides.github.com/activities/hello-world/)

Now, go ahead and create your first repository.  In the following example I will name my repository `final_project`.

![](../.gitbook/assets/screen-shot-2019-12-08-at-9.09.24-pm.png)

After creating your repository, go to the main page for your repository.  You should see a quick setup script under the `code` tab.  Click on `create a new file` under the quick set-up at the top of the page in order to populate your newly created repository with `README.md` file.  The `.md` extension after the filename is the extension for a markdown file.  Markdown is a simple, plain text formatting syntax language which has as its main design goal, as-is readability.   It is a relatively simple language that will enable you to program webpage content fairly easily. 

![](../.gitbook/assets/screen-shot-2019-12-08-at-9.56.08-pm.png)

This should bring you to a new page where you are able to create a new file.  In order for your GitHub Pages site to function properly, you will need a `README.md` file in the root folder of your repository.  Below the field for the file name is the markdown file body, where you will type your script.  Add a first level `header` to your `README.md` file by adding one `#` and following it with your title.  

![](../.gitbook/assets/screen-shot-2019-12-08-at-10.32.57-pm.png)

You can also preview the output from your markdown file, by clicking on the preview changes tab.

![](../.gitbook/assets/screen-shot-2019-12-08-at-10.33.05-pm.png)

After typing the simple markdown script, scroll to the bottom of the page and click on the green commit button, to commit your file to your repository.  You will need to press this green button, each time you edit the content within a file or add new files to your repository.  By making a new commit to your repository, you are essentially updating all of the changes you had previously made.  While in the case of your final project, there is essentially only one person executing changes per respository, potentially a version control system has the power of resolving conflicts amongtst multiple persons all committing changes to the same files simultaneously to the same respository.  That is the power of a version control system, such as GitHub.

![](../.gitbook/assets/screen-shot-2019-12-08-at-10.06.32-pm.png)

To begin getting an understanding of how to use markdown, have a quick look at the following cheatsheet.

{% embed url="https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet" %}

For the final project, you will only be using headers, paragraph text and inserting images and some animations to your GitHub pages site.  After having a look at the markdown cheatsheet, return to the main page of your repository, which should look like the following.  After navigating to that location, click on the `settings` tab in the top right hand corner.

![](../.gitbook/assets/screen-shot-2019-12-08-at-10.32.39-pm.png)

Scroll down to the GitHub pages section under settings and change the page source from `none` to `master_branch`.

![](../.gitbook/assets/screen-shot-2019-12-08-at-10.24.15-pm.png)

After setting the branch where your GitHub pages files will reside, also select the theme tab and choose one of the available themes.  I chose the theme `Caymen` for my page, but you are welcome to select any of the available themes for your final project.  After, selecting your theme and returning to the GitHub Pages section, you should notice a web address appear where your site has been published.  It might take a few moments for your webpage to appear, but not more than 10 or 15 seconds.  Usually it updates and publishes almost immediately.

![](../.gitbook/assets/screen-shot-2019-12-08-at-10.40.01-pm.png)

After clicking on the link, the newly created webpage that you will use to publish the results from your investigation should appear.  To start making changes to your website, go back to the main page of your repository and select the upload files tab.

![](../.gitbook/assets/screen-shot-2019-12-08-at-10.59.08-pm.png)

This should bring you to a page that will enable you to upload the images you have produced from each of the previous projects.  The interface should appear similar to the following image.

![](../.gitbook/assets/screen-shot-2019-12-08-at-10.58.00-pm.png)

I will begin by dragging and dropping a few of the plots produced that describe the administrative subdivisions of Liberia as well as the spatial distribution of it's population.

![](../.gitbook/assets/screen-shot-2019-12-08-at-11.04.22-pm.png)

After dropping the files into my repository, the basic file structure appears as follows.

![](../.gitbook/assets/screen-shot-2019-12-08-at-11.15.14-pm.png)

To add the image `details.png` to your `README.md` file, first select the `README.md` file, and then select the pen image in the upper right hand side of the screen to begin editing the content you already saved to your markdown file.

![](../.gitbook/assets/screen-shot-2019-12-08-at-11.17.44-pm.png)

After opening up the markdown file editor, add a second level header by preceding the text with two `##` and then add your image by adding a `![]` in advance of the file name `details.png` , which is contained within `()` .  Don't forget to scroll down to the bottom of the page and click on the commit button to make sure the changes you have made to the file are properly committed to the repository.  If you do not commit your changes to your repository, your file will not have been saved nor published.

![](../.gitbook/assets/screen-shot-2019-12-08-at-11.25.56-pm.png)

After committing the changes and waiting a few moments, your changes will appear to the published webpage.

![](../.gitbook/assets/screen-shot-2019-12-08-at-11.28.27-pm.png)

After adding your map that describes the political subdivisions of your LMIC, also add your description of population as spatially distributed at different adm levels.

![](../.gitbook/assets/screen-shot-2019-12-09-at-3.25.56-am.png)

If you created a animated video, such as a `.mp4` file that rotates and describes population in three dimensions, you will need to convert that file to a `.gif` in order to include in your project webpage.  This is fairly easily accomplished by using an online conversion tool.  I simply entered "online conversion of mp4 to gif mac" into google, and google returned several possible options, such as [https://ezgif.com/video-to-gif](https://ezgif.com/video-to-gif), among many.  After converting your `.mp4` to a `.gif` , upload the file to your repository and include it in your markdown file.

![](../.gitbook/assets/screen-shot-2019-12-09-at-3.34.14-am.png)

Which will produce the following image as part of your webpage.

![](../.gitbook/assets/pop.gif)

{% embed url="https://wicked-problems.github.io/final\_project/" %}

## Final Individual Deliverable

Produce a webpage using GitHub pages and markdown that describes your investigation through the course of the semester.  Include in your final product sections that answer the following questions.

1.  Describe the **political subdivisions** of your LMIC and selected administrative subdivisions.  Use a spatial description of the political subdivisions of your LMIC at the first, second and/or third administrative levels as appropriate and identify the location of your selected administrative subdivisions. Provide a detailed, spatial description of the political subdivisions that describe your selected administrative areas.
2. Describe the **population** of your LMIC and selected administrative subdivisions.  Spatially describe the population distribution of your LMIC at the first, second and/or third administrative levels as appropriate.
3. Provide the results from your analysis of your LMIC's population including validation of the predicted spatial distribution of population values at different scales and your interpretation of relevant model results.
4. Provide results from your description of the _de facto_ location of **human settlements** and urban areas, the center lines of classified **roadways** and the location of **health care facilities** by type throughout your selected and combined adm2, adm3 or adm4 areas.

Include with the relevants plots your interpretation and analysis as well as supplemental tables and charts that further support your findings.  Be comprehensive in your approach to developing your webpage.  If you transitioned from country or location to another country or location due to technical issues, simply provide some justification as to why and how that transition took place.

Upload a link to your individual final project to the slack channel \#data100\_project4 no later than 5:00PM on Tuesday, November 26th.  Your team will present an extended, comparison of your selected administrative areas within each LMIC, during the final group presentation, held on either December 4th or December 6th.

