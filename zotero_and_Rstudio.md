## Writing Academic Papers using R Studio + Zotero (and optionally, connect to GitHub)

Writing tutorials, reports, and papers in markdown is a pleasant experience because of the easy incorporation of text, code, and images without the need to rely on word processing software. However, I've still been writing most of my journal articles and other research outputs using Microsoft Word. The main reason is because I rely heavily on my Zotero library to manage my collection of references, and Zotero has relatively okay intergration with word (well, sometimes it breaks). 

I'm a bit late to the party, but I've recently found that R Studio has some very painless integration with Zotero that allows for library searching via the citation picker. This means one can have the best of both words - writing in markdown *and* having integrated access to their zotero library. It takes only a minor bit of setting up, but I'll write this process up here for those who might be interested in ditching Word and using two great open source programs to writing your academic papers. But first, I'll give some brief motivation for why how I've found Zotero to be a critical part of my academic writing process.

### How Zotero integrates with MS Word/others

I know that I could write papers in LaTeX (or markdown) using bibtex and manually write all my citations like this `\citep{deadauthor1927}`, but I have always found that to be disruptive to my writing flow *and* requires an encyclopedic level of the references I might want to connect to a certain point. This is why I am chained to the Zotero picker method for citing in word. For example, let's look at a sentence from a recent manuscript I'm still working with:

***

![](https://i.imgur.com/OKijBzD.png)
***

As a good little academic, I should probably add some references to the end of this sentence, primarily to ensure this claim has some justification, but I also plan to cite myself here because this is referring to some prior work I've done. I have a good idea of which papers I'd like to cite, but I want to make sure I'm getting the most appropriate citations here. This is where Zotero's citation picker really shines. Since my memory is...*questionable*...I can search the Zotero picker for papers which have my name:

***

![](https://i.imgur.com/Kjv4WcW.png)

***

Cool! I could use this to scroll through and refresh my memory for each paper I'm interested in citing. Alternatively, I could use key search terms related to the topic which will cast a wider net to find more articles:

***

![](https://i.imgur.com/t8wsfy0.png)

***

Hopefully you get the idea - having this sort of quick integration to my reference library *while* writing is a huge boon to my writing flow and one I simply cannot give up. The Zotero picker is also available when using Zotero in other supported word processing software programes, as well as Google Docs. For me, having the Zotero picker is thus an acceptable tradeoff for not being able to write using markdown. Until now!

### Using Zotero in R Studio
R Studio continues to impress as an all-in-one IDE for doing analyses with R. R Studio also allows for a flavour of markdown called R Markdown, which as far as I know is markdown tuned to run R code cells. I've recently decided to challenge myself and complete a major writing project within R Studio using R Markdown. The only way I could do this was if I could have access to the Zotero reference picker, which I have only recently found out is possible in R Studio! (I guess I should read their blog more). I'm going to quickly outline what you need to do in order to get the picker working in R Studio so you can determine if you'd like to use this method for your own papers. You *can* also use the Zotero picker with markdown using a [VS Code plugin](https://marketplace.visualstudio.com/items?itemName=mblode.zotero), and if you already use VS Code a lot in your workflow that might be handy.

#### Step 0. Prerequisites

You should have R Studio version 1.4 or greaterand Zotero desktop installed on your computer, and have some references already in Zotero. Maybe this is a good opportunity to prompt you to update both programs! If you want to connect to github, you should have a github account and know how to make a repository.

#### Step 1. Get Better BibTeX into Zotero

BetterBibTeX is a Zotero plugin designed to allow for "easier" integration between Zotero and markdown/LaTeX authoring. You can find the instructions to [download BetterBibTeX here](https://retorque.re/zotero-better-bibtex/installation/), which will be in the form of a Zotero plug in. Download the latest `.xpi` file, then open up Zotero desktop, choose tools, then choose addons, click the gear in the top right (at least on Mac, not sure if the windows version looks the same) and choose to install an addon from file. You can see below that I've got a few other addons, including the plugins that allow Zotero to work with some word processors. 

***

![](https://i.imgur.com/F3OralY.png)

***

That's pretty much it - If you have R Studio 1.4+, then it will [automatically detect your Zotero library](https://rstudio.github.io/visual-markdown-editing/citations.html), how easy is that? 

#### Step 2. Create a project with R Studio (optional: connect to GitHub)

I'd strongly recommend creating a new R Studio project, because R Studio is going to use Zotero to create a `.bib` file and you'll want these files to be in the same folder. 

To go the extra step, you could create a project using git so that you can use R Studio to push your changes to github (you can skip this step if you like). 

#### Project w/o GitHub integration

If you create a regular project, it will look something like this:

***

![](https://i.imgur.com/mGq6Uwb.png)

***

#### (Optional) Project w/ GitHub integration

To connect to a github repo, go ahead and make a github repo for this project, then copy the https URL for connecting to the repo. 

Then, choose to make a new R Studio project with version control, then choose git, then enter your repo url:

***

![](https://i.imgur.com/W0rgSJk.png)

![](https://i.imgur.com/CxfZNMy.png)

![](https://i.imgur.com/7dXzbsP.png)

If all goes well, R Studio should clone into the repository and you should see the git options in the environment pane of R Studio, as well as the git files in the file viewer:

![](https://i.imgur.com/a4MUejL.png)

If you have not connected via R Studio before, you will likely need to authenticate, which means creating either a [personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) or [ssh key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/about-ssh).

I have experienced a few issues with this primarily because I have used more than one github account through R Studio and setting the credentials can get messy. If you're familiar with bash and command line git, you can always use the terminal within R Studio to try to sort these things. However, I've found that if you use the HTTPS method of cloning into a repo, you can append your username to the URL to at least avoid some credentialing issues:

***

![](https://i.imgur.com/iyGpTQ8.png)

***

Once your project is created, go ahead and make a new markdown document and save it (I saved mine by naming it `zotero`). Note that when you make a new file using R Studio's file --> new document menu, you'll provide a name in the GUI but that name is used for the yaml header and *not* the name of the file - you'll have to manually save the file after this step to name the file itself (I always find this a bit annoying, maybe I'm doing it wrong?).


![This "title" is only for the yaml!](https://i.imgur.com/RSWxr6f.png)


Anyhow, after doing this, if you click "OK" R Studio will create a markdown file with a prepopulated yaml header, code cell, and some other basic instructions on how to use markdown (click "create empty document" to avoid this). It will look something like this.  

***

![](https://i.imgur.com/EJ7nkqK.png)

***

If you're using a GitHub connected project, now is a good time to test if you can push to your repo. You should see your new markdown file in the github environment pane:

![](https://i.imgur.com/Ms4HT1y.png)

The yellow ? means the files aren't being tracked for changes. You can click "staged" to tell R Studio you'd like to track changes to these files for your commit. You can also apend your `.gitignore` file to remove files from thie pane (I find it annoying that the `.Rproj` and `.gitignore` files sit there). Since you can see your `.gitignore` file in the file viewer, just click on it to open and you can add more files to this list. I've added the two files I've just mentioned as well as any files ending in pdf, docx, or html extensions, since we'll be creating those while knitting the markdown, and I don't need to upload those as part of the project:

![](https://i.imgur.com/fFWNe4w.png)


After you've updated and saved the `.gitignore` file, click the refresh listing button in the git pane and you should only see the markdown file:

![](https://i.imgur.com/PKgZZTA.png)

Now, select to stage the file, and the icon next to your markdown file should change to an "A" for added:

![](https://i.imgur.com/2gRbSN9.png)

Click commit and enter a commit message like you normally would:

![](https://i.imgur.com/yiAcZda.png)

You should be able to commit:

![](https://i.imgur.com/5mtZ43y.png)

And then use the green up arrow to push:

![](https://i.imgur.com/nqama67.png)

Voila:

![](https://i.imgur.com/SBhiufi.png)

Now, I have experienced GitHub hell in R Studio a few times, which is why this step is optional. But when it works, it can be very convenient to have the GUI and stage commits and pushses all from the same program you are writing code and markdown in. You can always use the command lines to push/pull if you prefer.

#### Step 3. Adding some citations

Okay, now that we've got a markdown file in R Studio and a project set up (optionally connected to GitHub), let's get on with putting in some citations! To do so, let's first switch to the necessary view introduced with R Studio 1.4 which is a "visual markdown editor", you can click the gear in the pane and switch to the visual editor or click the "A" looking button on the far right of the menu bar:

![](https://i.imgur.com/6e1gmnS.png)

The visual editor is now a WYSIWYG markdown editor within R Studio...very cool. I've deleted all the pre-populated markdown and added the same sentence from my word doc above to the markdown file (I've also enabled spell-checking in the R Studio options):

![](https://i.imgur.com/4Ib2kpI.png)

Now, I can click "insert" and see that one of the options is citations!

![](https://i.imgur.com/CX8DvQr.png)

Clicking the @ Citation option will open the screen where you *should* see your Zotero library (and a few other resources). Note that the references have been converted using BetterBixTex to conform with markdown citations. Just like the picker in word, you can search your library using author names or key terms. 

![](https://i.imgur.com/z2OoWk5.png)

Note that you can also just search databases directly to find resources *not* in your Zotero library - wow!

![](https://i.imgur.com/SohV7Mh.png)

Note at the bottom there is the option to "create bibliography", and this is how R Studio will integrated with BetterBixTex to keep your citations happy. I chose a `.yaml` file with csl but the default will be a `.bib` file. You see, if you were to use Zotero with another markdown program (like VS Code) you'd need to import your entire `.bib` file to wherever your markdown program is, and export it everytime you update your zotero library. Because R Studio will make a new `.bib` file for you each time, it becomes seamless and you should never get an error when knitting related to not having a reference in your bibliography!

Ok, let's add in a citation. I'll choose one of my papers from the graphical interface and click ok:

![](https://i.imgur.com/aS83iZX.png)

Easy, it's just inserted the citation in markdown format for me, so nothing fancy there. But, can we get the Zotero picker *while typing*? The answer is yes! If we start typing a citation with '@', a different format of the picker will appear, searching through the BibTeX keys associated with the references:

![](https://i.imgur.com/7ZY99ri.png)

Now, this is clearly not the same as the Zotero picker for word, because our search here is limted to the citation key. But, it's *close enough* for me to be able to use the graphical search via the 'insert citation' shortcut that I'll take it. 

Anyhow, I've added two citations, one in full parenthetical format (Author, Year), and one for in-text: Author (Year):

![](https://i.imgur.com/XFbdPU8.png)

If you click "knit" on the toolbar, R studio will now convert your markdown to html, and you can see the results in the R Studio viewer:


![](https://i.imgur.com/BoAe97R.png)

The `.html` file will alow be created within the same directory. You can change your `.yaml` header to control the default knit behaviour, or click the small arrow next to knit and choose the output that way, allowing you to knit to word and pdf, and the files will be automatically added to your folder (this is why I added those file extensions to my `.gitignore` file earlier).

![](https://i.imgur.com/dspu8yv.png)

You can also add your citations via markdown using the "regular" markdown editor and not the visual editor in R Studio, but you will lose the contextual help pop-ups that I think make the visual editor worthwhile. 

#### Step 4. Changing your reference style

One of the major advantages of using Zotero is that you can customize your referencing style via a wide range of pre-existing templates, saved as .csl files. You can search the database of .csl files on the [Zotero Styles Repository](https://www.zotero.org/styles). For my project, I would like to use APA 7th, so I simply search and download the .csl file:

![](https://i.imgur.com/rdFAcYg.png)

The website will ask you if you want to add it directly to Zotero, which you may want to do, but you also want the actual .csl file, so it might be easier to right click and save as, and direct the .csl file to your R Studio project folder. 

Here is what my files look like after knitting to word, pdf, html, and downloading the .csl file. 

![](https://i.imgur.com/u1VBRzp.png)

My reference list is in some format I don't want:

![](https://i.imgur.com/NcdSxY0.png)

To change the referencing to APA 7th, I simply add the .csl file as a new property to my yaml header:

![](https://i.imgur.com/XSmxs73.png)

Knit the document again, and my references are now in lovely APA 7th:

![](https://i.imgur.com/kXsNQsU.png)

Once I'm done writing for the day, I can toss a commit and push to my repo and call it done - saving not only my writing, but my reference list and any style .csl files! I'm still fresh into this new workflow, but think this will be a huge benefit for authoring articles and reports all directly from on central location. 

I can also take an .md file I've authored elsewhere (such as this one), toss it into the project, and R studio will have no problem rendering it :)

You can read more about Zotero integration with R Studio [here](https://rstudio.github.io/visual-markdown-editing/citations.html).
