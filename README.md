# <a name="top"></a>aero-structures
Resources for analyzing aerospace (i.e. aircraft, rocket, spacecraft) structures for aerospace engineers.

# <a name="scope"></a>Scope
This page provides resources for the analysis aircraft structures using classical methods developed by prominent engineering minds such as Elmer F. Bruhn, Michael Niu, Warren Young (aka Raymond J. Roark), and Sighard F. Hoerner. This page also includes applications of these analysis methods in Python. Finite element methods are mentioned to provide context, but are otherwise not within the scope of this page

Ultimately, my objective is to:
* Create a portal for standard structural analysis methods used in the aerospace industry
* Help you learn how to [save time](https://xkcd.com/1205/) with examples of how I automate and optimize routine analysis with Python
* Provide you with a template to document your own engineering processes & analysis tools in a meaningful way

**Note:** To keep this document free of implicit endorsement, there are no links to Amazon, Google, etc. They're easy enough for you to use on your own to find the materials you want.

**Disclaimer:** All content on this page is provided on a strictly informational basis. The contributors to this page cannot assume any responsibility, in any manner whatsoever, for the use readers make of the information presented herein, or the devices, systems, or calculations resulting therefrom. It is the responsibility of the reader to determine if the data and information provided are in agreement with the latest design allowables.

# <a name="rationale"></a>Rationale
Analysis engineers face two different, but interrelated challenges when working 

1. Communicate analysis and findings to their colleagues, managers, and clients in a way that effectively conveys information to the intended audience.
1. Internally documenting the numerous analyses, processes, and tools used throughout a project in a meaningful and accessible way for later reference, often by engineers other than the original ones who developed them.

There have been a number of times where I completed a project, and some months or even years later started another, similar project. When I refer to the old project files, I find that it's disorganized at best, often missing key pieces of information that aren't immediately obvious. This isn't intensional, of course -- it's simply the result of the engineer being forced to sacrifice some level of documentation to get work product out the door, which is an unfortunate reality of schedule-driven projects.

This means I have to spend a significant amount of time re-developing processes and tools to ensure that all the relevant parts are in place to succeed in the new project. As projects scale in complexity, this _mobilization cost_ becomes greater, and it's worth taking steps in an attempt to reduce it. This page is a first step in documenting analysis tools that I frequently use, and hopefully serve as a template for you to do the same.

New graduates will encounter moments in their career where they ask themselves, *"Why didn't I learn this in school?"* during their formative years as an EIT. My hope is that some of these resources will accelerate the learning process, and potentially save inexperienced engineers from committing serious but preventable mistakes.

Another, more aerospace-specific problem has been happening for several decades now. While there are many resources for aerospace engineering, much of it is scattered about disparate places around the net (e.g. countless threads on [Eng-Tips](http://www.eng-tips.com/)), or locked behind proprietary sources like the _Boeing Design Manual_. The aerospace industry has a lot of "tribal" knowledge that becomes lost when veteran engineers, technicians, mechanics, and fabricators retire or pass away without disseminating their decades of experience and knowledge to the next generation. There's simply no replacement for this knowledge, and very little of it makes it into modern aerospace texts, let alone university lecture halls. Even when this knowledge is documented in company design manuals, in the end they are only manuals and do not effectively replace an experienced mentor.

[⇪ Top](#top)

---

# <a name="toc"></a>Table of Contents
<details open><summary><sup>Hide</sup>/<sub>Show</sub></summary><br/>

- [Symbols & Abbreviations](#symbols)

- [Universal References](#u-references)

- [Python References](#py-references)
  - [Beginner-Novice](#beginner-novice)
    - [Why Python?](#why-python)
    - [Learning Python for the First Time](#learning-python-for-the-first-time)
  - [Intermediate-Advanced](#intermediate-advanced)

- [](#)

[⇪ Top](#top)
</details>

---

## <a name="symbols"></a>Symbols & Abbreviations

<details close><summary><sup>Show</sup>/<sub>Hide</sub></summary><br/>

Nomenclature|Definition
:---:|:---
AN|Army-Navy Standard
FEA|Finite Element Analysis
FEM|Finite Element Model
IDE|Integrated Development Environment; e.g. _Spyder_, _JupyterLab_, _Sublime Text_
MIL|Military; see MS
MMPDS|Metallic Materials Properties Development and Standardization; see [Universal References](#u-references)
MS, MIL-STD|Military Standard
PEP|Python Enhancement Proposal; e.g. [PEP8](https://www.python.org/dev/peps/pep-0008/)

</details>

---

## <a name="u-references"></a>Universal References
These references are universal in that they are frequently used by aerospace design engineers to conduct analysis during the preliminary and detail design phases. While FEA is a powerful analysis tool, it comes with a lot of costs and overhead that isn't practical or necessary for a lot of engineering problems. In many cases a problem can be solved using a straightforward analysis process out of one of these texts, and if necessary, automated using a Python script. A common glib in engineering goes: *"Someone a lot smarter than me figured this out 50 years ago."* — which is really just another way of saying *"Don't re-invent the wheel."*

**Students beware:** Most of these resources are not suitable for learning topic/course material for the first time.

### <a name="mmpds"></a>Metallic Materials Properties Development and Standardization (MMPDS)
MMPDS is a database of statistically-verified strength data for common aerospace materials and fasteners, which serves as the basis for design manuals in nearly every aerospace company. While a new version of MMPDS with updated data gets released every year or so, older versions remain valid for aerospace design work. MMPDS-01 is available for free from the [National Technical Reports Library](https://ntrl.ntis.gov/NTRL/dashboard/searchResults/titleDetail/PB2003106632.xhtml) (U.S. Dept. of Commerce).

**Note:** For aerospace design, MMPDS supersedes MIL Handbook. MMPDS-01 contains data equivalent to MIL-HDBK-5J.

### <a name="bruhn"></a>"Analysis and Design of Airplane Structures" by Elmer F. Bruhn
Considered by many to be 'the Bible' of flight vehicle analysis, Professor Bruhn detailed empirical design methods and calculation processes for aircraft structures that were used for practically every aircraft design from the 1940s and onward, until the advent of FEA and computer-driven numerical methods in the mid-1970s. This book no longer appears to be published, so if you find a copy, buy it.

### <a name="niu"></a>"Airframe Structural Design: Practical Design Information and Data on Aircraft Structures" by Michael Niu
Niu was the Senior R&D Engineer at Lockheed Martin and Stress Engineer at Boeing Co. during the development of the 727 and 747. With over 30 years of experience, Niu wrote about nearly every detail design consideration required for flight vehicle design. This text contains helpful diagrams and practical examples from his work, backed by empirical data & charts that can be referenced for various stress coefficients for specific types of analysis.

### <a name="roark"></a>"Roark's Formulas for Stress and Strain" by Warren C. Young & Richard G. Budynas
Known better under his pen name Raymond J. Roark, Professor Young draws upon more than four decades of academic research in mechanics of materials and mechanical engineering to produce one of the most commonly referenced engineering books of all time. While not aerospace-specific, *Roark's* is invaluable for the analysis and detail design of many types of mechanical loading problems.

### <a name="hoerner"></a>"Fluid-Dynamic Lift" and "Fluid-Dynamic Drag" by Sighard F. Hoerner
Following World War 2, the aerodynamics field exploded with pioneers and researchers like Dr. Hoerner leading the field. In the same way that Professor Bruhn's text is go-to reference for the analysis of flight vehicle structures, Hoerner's books are absolutely fundamental for aerodynamic analysis of all kinds.

### <a name="dtic"></a>[Defense Technical Information Center (DTIC) ASSIST-QuickSearch](https://quicksearch.dla.mil/qssearch.aspx)
For all your MIL-spec needs. Preferable over unofficial sites like EverySpec. Document ID is something like `MIL-HDBK-5`, or you can search using comma-separated strings.

### <a name="ntrs"></a>[NASA Technical Reports Server (NTRS)](https://ntrs.nasa.gov/search.jsp)
NTRS contains a vast wealth of information dating back to the early days of NASA, when they were known as the _National Advisory Committee for Aeronautics (NACA)_ from 1915 to 1958. Major topics of interest include both aeronautics and aerospace research, such as NACA airfoil test data; aerodynamic test data; flight vehicle design manuals; and design manuals on rocket staging, propellants, etc.

When searching NTRS, I recommend having a very specific query on a design or analysis problem — there's a decent chance that someone at NASA has already done the legwork for you. An example of a good query is `buckling thin shell` and `double slotted flap`. I also suggest filtering the `Document Type` to only contain "Technical Reports", which will only show NASA design manuals and technical memos.

Documents of interest on various topics:

* [NASA-SP-125: "Design of Liquid Propellant Rocket Engines, Second Edition" by D.H. Huang & D.K. Huzel](https://ntrs.nasa.gov/search.jsp?R=19710019929)
* [NASA-RP-1228: "Fastener Design Manual" by Richard T. Barrett](https://ntrs.nasa.gov/search.jsp?R=19900009424)
* [NASA-SP-8007: "Buckling of thin-walled circular cylinders" by Peterson-Seide-Weingarten](https://ntrs.nasa.gov/search.jsp?R=19690013955)

---

## <a name="py-references"></a>Python References

This section assumes that you have zero programming knowledge. Your goal here is to go from `Hello world!` to what Chris Moffitt calls the ["plateau of productivity"](http://pbpython.com/plateau-of-productivity.html).

[<img src="./images/hype-cycle.png" width="559">](http://pbpython.com/plateau-of-productivity.html)

Many people who start coding for the first time get stuck in the "trough of disillusionment" stage of learning, and struggle to break out of it. I pushed a boulder up this same hill many times, only to fall back into the trough and give up for a while... but after numerous tries and lots of encouragement from my friends, learning partners, and the Python community, I got past the rut and now routinely develop my own engineering tools. It has absolutely been worth all the effort — not only in the time Python has saved me, but also in the sense of accomplishment.

Randall Munroe (xkcd) came up with a handy chart for figuring out whether or not it's worth spending your time automating a given task.

[<img src="./images/is_it_worth_the_time_2x.png" width="618">](https://xkcd.com/1205/)

### <a name="why-python"></a>Why Python?
* It's easy to learn and a great first coding language.
* It's a mature language with a vibrant, active open-source community. There are thousands of useful libraries that tend to be well-documented.
* It's used for many applications such as scientific computing, web development, data analysis, and machine learning.
* It can be extended into C/C++ for embedded computing applications.

### <a name="beginner-novice"></a>Beginner-Novice
Whether you're learning to code for the first time or an experienced programmer looking to add Python to your repertoir of languages, these resources will get you up and running quickly. The very first thing you'll want to do is download the [Anaconda distribution](https://www.anaconda.com/download/) of Python 3, and start up an IDE of your choice for one of the resources below. I recommend _JupyterLab_ or _Spyder_

#### <a name="learning-python-for-the-first-time"></a>Learning Python for the First Time
There are five main resources recommended by the Python community, all of them free. You only need to choose one and stick with it, but as we are all blessed with different minds, you'll want to try several to see which is more suited to your learning style. As one of my professors once told me, *"Find a voice that speaks to you."*

1. [Automate the Boring Stuff with Python](http://inventwithpython.com/#automate) by Al Sweigart
1. [Dive into Python 3](http://www.diveintopython3.net/) by Mark Pilgrim
1. [Think Python](http://greenteapress.com/wp/think-python-2e/) by Allen B. Downey
1. [Python 101](http://python101.pythonlibrary.org/index.html) ([ebook version here](https://leanpub.com/python_101)) by Michael Driscoll
1. [The Official Python Tutorial](https://docs.python.org/3/tutorial/index.html) by the Python Software Foundation

All of them cover the basics of Python, but don't completely overlap with each other in the topics they cover. The main difference is that 1 & 2 get you off the ground faster, giving you the knowledge to start writing practical programs very quickly, while 3-5 take longer to get through, but are more comprehensive and focus on helping you build a solid foundation in Python. It's completely fine to go with one of the faster resources and fill in the gaps later as you need to.

I like *"Automate the Boring Stuff with Python"* the best, which took me about 50 hours (and numerous tries) to get through. At some point early on, you'll start to get the itch to write real programs. That's perfectly normal, and I encourage you to start applying what you've learned using a project-based approach. Finding problems and coming up with a solution in Python is the best way to remember and apply the concepts you've learned — and ultimately get better at programming — rather than spending all your time reading and watching videos.

One resource you should avoid is *"Learn Python the Hard Way"* by Zed Shaw, mainly because it's outdated.

#### <a name="code-like-a-pythonista"></a>[Code Like a Pythonista: Idiomatic Python](http://python.net/~goodger/projects/pycon/2007/idiomatic/handout.html)
As you learn Python, you'll start to understand why styling and whitespace are important. David Goodger's *"Code Like a Pythonista"* and similarly [PEP8](https://www.python.org/dev/peps/pep-0008/) are important companions to have so that you get into the habit writing readable code. While you can afford to skip over some bits of the Python language to learn later, you can never afford to write crappy code because it can (and will) come back to bite you later. The most confused engineer is frequently the same person who wrote the code, looking at it months or years later.

As [SICP](https://mitpress.mit.edu/sicp/full-text/book/book-Z-H-7.html) wisely stated:

> \[...] a computer language is not just a way of getting a computer to perform operations but rather \[...] it is a novel formal medium for expressing ideas about methodology. Thus, programs must be written for people to read, and only incidentally for machines to execute.

Or as [The Zen of Python](https://www.python.org/dev/peps/pep-0020/) simply says: __Readability counts.__

#### <a name="pbpython"></a>[Practical Business Python](http://pbpython.com/)
PB Python is a monthly-ish blog by Chris Moffitt ([@chris1610](https://github.com/chris1610/pbpython)) where he talks about how to apply Python in an everyday business setting. This is the best resource I've found for contextualizing how Python can be used as a powerful tool for enhancing or eliminating tasks that are normally done using Excel or Word. It's also a great place to get started with `pandas` (Python Data Analysis Library) for the first time, which should be of interest for Test/Instrumentation Engineers and Flight Test Analysts.

Head into the [PB Python Archive](http://pbpython.com/archives.html) and start with the article from 5 October 2014, ["Using Sets for Data Analysis"](http://pbpython.com/data-analysis-with-sets.html). As you move forward, go through the articles in chronological order. Chris does a fantastic job of building upon each one until you have a formidable set of tools to tackle a variety of problems!

**Note:** For planning purposes, each PBpy exercise can take 1-2 hours to get through, depending on the topic and your skill level.

#### <a name="regex101"></a>[Regular Expressions 101](https://regex101.com/) by Firas Dib
Regular expressions are a powerful tool, but can be hard to dive into while learning Python. You should practically consider it as a separate language. This regex tester and repository is a great resource that can get the regex you need into your Python applications, while also explaining how the specific regex works.

#### <a name="learning-python"></a>"Learning Python, 5th Ed." by Mark Lutz
This text is perhaps the most comprehensive resource for beginner Python users, and covers some topics that aren't in any of the [Learning Python for the First Time](#learning-python) resources, such as interfacing Python with C/C++. This is of particular interest for engineers that work with embedded systems that require C/C++, or anyone that desires the computational power of C/C++ while keeping the ease of development in Python.

Since this book is an absolute behemoth of over 1,600 pages, I recommend it mainly as a companion reference for looking up concepts & examples that aren't explained thoroughly by any of the free resources. For even more exercises, Mark Lutz made his [live course materials](http://learning-python.com/training) available for free.

#### <a name="python-in-a-nutshell"></a>"Python in a Nutshell" by Martelli-Ravenscroft-Holden

---

### <a name="intermediate-advanced"></a>Intermediate-Advanced
By the time you've completed some programming projects on your own, you'll probably need some resources to reach the next skill level as a Python developer. The books in this section will help correct some of the bad habits you've undoubtedly picked up while learning Python, and fill in any knowledge gaps while also delving into more advanced programming methods. "Fluent Python" is a solid and frequently recommended text that you can't go wrong with, but each of these books has something different to offer depending on what your learning goals are.

#### <a name="fullstackpython"></a>[Full Stack Python](https://www.fullstackpython.com/introduction.html)
Full Stack Python is a landing point for intermediate Python learners looking for a specific focus or application. This open book includes a wealth of resources for getting into web development, data analysis, security, and application deployment, which can be helpful for coming up with projects and learning goals beyond mastering the language.

#### <a name="fluent-python"></a>"Fluent Python: Clear, Concise, and Effective Programming" by Luciano Ramalho

#### <a name="effective-python"></a>"Effective Python: 59 Specific Ways to Write Better Python" by Brett Slatkin

[From the author of "Effective Python" on the differences from "Python Cookbook"](https://www.reddit.com/r/Python/comments/31zjy5/book_effective_python_vs_python_cookbook_which/cq6nl66/):

> Author of Effective Python here. I think they're very different books! David Beazley is awesome and a wonderful educator. He's always the best speaker at PyCon. I'd say: the _Cookbook_ is a powerful and thorough reference, the _Effective_ books are short and scenario driven.

#### <a name="python-cookbook"></a>"Python Cookbook" by David Beazley and Brian K. Jones

#### <a name="high-performance-python"></a>"High Performance Python: Practical Performant Programming for Humans" by Micha Gorelick and Ian Ozsvald

#### <a name="hackers-guide-to-python"></a>"The Hacker's Guide to Python" by Julien Danjou

---
