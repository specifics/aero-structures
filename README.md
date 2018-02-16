# <a name="top"></a>aero-structures
Resources for analyzing aircraft structures for aerospace engineers.

# <a name="scope"></a>Scope
This page provides resources for the analysis aircraft structures using classical methods developed from prominent engineering minds such as Elmer F. Bruhn, Michael Niu, Warren Young (aka Raymond J. Roark), and Sighard F. Hoerner. FEA methods are not covered. This page also includes methods to port these methods into Python 3, allowing engineers become more effective at their job by rolling their own code and interface with other engineers in a professional environment.

Ultimately, this page should:
* Be a portal for non-FEA structural analysis methods used in the aerospace industry
* Help you [save time](https://xkcd.com/1205/) by automating & optimizing routine analysis in Python
* Provide you with a template to document your own engineering processes & tools in a meaningful way

**Note:** To keep this document free of implicit endorsement, there are no links to Amazon, Google, etc. They're easy enough for you to use on your own to find the materials you want.

**Disclaimer:** All content on this page is provided on a strictly informational basis. The contributor(s) to this page cannot assume any responsibility, in any manner whatsoever, for the use readers make of the information presented herein, or the devices, systems, or calculations resulting therefrom. It is the responsibility of the reader to determine if the data and information provided are in agreement with the latest design allowables.

# <a name="rationale"></a>Rationale
Engineers frequently have to communicate analysis and findings to their colleagues, managers, and clients. A problem occurs when the engineer fails to communicate effectively for the intended audience, and also when he or she doesn't document their process in a meaningful and accessible way for later reference. As programmers quickly learn, the person who's most likely to be confused when reading your code is your future self. This page is a first step in documenting analysis tools that I frequently use, and hopefully serve as a template for you to do the same.

Another, more aerospace-specific problem exists for professional engineers and students. While there are many resources for aerospace engineering, much of it is scattered about disparate places around the net (e.g. countless threads on [Eng-Tips](http://www.eng-tips.com/)) and around the world. The aerospace industry in particular has a lot of "tribal" knowledge that becomes lost when veteran engineers, mechanics, and fabricators retire or pass away without disseminating their decades of experience and knowledge to the next generation. There's simply no replacement for this knowledge, and very little of it makes it into modern aerospace texts, let alone the lecture hall. Even when this knowledge is documented in design manuals, they are no replacement for an experienced mentor.

For students, this is problematic when trying to attain the requisite knowledge to enter a very limited and competitive job market. Some of these resources will address the *"Why didn't I learn this in school?"* moments that new engineers will almost certainly encounter during their formative years. Hopefully these resources will accelerate that learning process and save young engineers from committing serious but preventable mistakes.

[⇪ Top](#top)

---

# <a name="toc"></a>Table of Contents
<details open><summary><sup>Hide</sup>/<sub>Show</sub></summary><br/>

- [Symbols & Abbreviations](#symbols)

- [Universal References](#u-references)

- [Python References](#python-references)
  - [Beginner-Novice](#beginner-novice)
    - [Why Python?](#why-python)
    - [Learning Python for the First Time](#learning-python-for-the-first-time)
  - [Intermediate-Advanced](#intermediate-advanced)

- [](#)

[⇪ Top](#top)
</details>

---

## <a name="symbols"></a>Symbols & Abbreviations

<details open><summary><sup>Hide</sup>/<sub>Show</sub></summary><br/>

Nomenclature|Definition
:---:|:---
AN|Army-Navy Standard
FEA|Finite Element Analysis
MIL|Military; see MS
MMPDS|Metallic Materials Properties Development and Standardization; see [Universal References](#u-references)
MS|Military Standard
PEP|Python Enhancement Proposal; e.g. [PEP8](https://www.python.org/dev/peps/pep-0008/)

</details>

---

## <a name="u-references"></a>Universal References
These references are universal in that they are frequently used by aerospace stress engineers to conduct basic & advanced analysis. While FEA is a powerful analysis tool, it comes with a lot of costs and overhead that isn't practical or necessary for a lot of engineering problems. In many cases a problem can be solved using a straightforward analysis process out of one of these texts, and if necessary, automated using a Python script. A common glib in engineering goes: *"Someone a lot smarter than me figured this out 50 years ago."* — which is really just another way of saying, *"Don't re-invent the wheel."*

**Students beware:** Most of these materials are not suitable for learning course material for the first time.

### <a name="mmpds"></a>Metallic Materials Properties Development and Standardization (MMPDS)
MMPDS is a database of statistically-verified strength data for common aerospace materials and fasteners, which serves as the basis for design manuals in nearly every aerospace company. While a new version of MMPDS with updated data gets released every few years, older versions remain valid for aerospace design work. MMPDS-01 is available for free from the [National Technical Reports Library](https://ntrl.ntis.gov/NTRL/dashboard/searchResults/titleDetail/PB2003106632.xhtml) (U.S. Dept. of Commerce).

SHA256 hash for MMPDS-01: `4e252754c126d71d877222b80dba0a0641acc672e1052a7844058ada009118de`

**Note:** For aerospace design, MMPDS supercedes MIL Handbook. MMPDS-01 contains data equivalent to MIL-HDBK-5J.

### <a name="bruhn"></a>"Analysis and Design of Airplane Structures" by Elmer F. Bruhn
Considered by many to be 'the Bible' of flight vehicle analysis, Professor Bruhn detailed empirical design methods and calculation processes for aircraft structures that were used for practically every aircraft design from the 1940s and onward, until the advent of FEA and computer-driven numerical methods in the mid-1970s. This book no longer appears to be published, so if you find a copy, buy it.

### <a name="niu"></a>"Airframe Structural Design: Practical Design Information and Data on Aircraft Structures" by Michael Niu
Niu was the Senior R&D Engineer at Lockheed Martin and Stress Engineer at Boeing Co. during the development of the 727 and 747. With over 30 years of experience, Niu wrote about nearly every detail design consideration required for flight vehicle design. This text contains helpful diagrams and practical examples from his work, backed by empirical data & charts that can be referenced for various stress coefficients for specific types of analysis.

### <a name="roark"></a>"Roark's Formulas for Stress and Strain" by Warren C. Young & Richard G. Budynas
Known better under his pen name Raymond J. Roark, Professor Young draws upon more than four decades of academic research in mechanics of materials and mechanical engineering to produce one of the most commonly referenced engineering books of all time. While not aerospace-specific, *Roark's* is invaluable for the analysis and detail design of many types of mechanical loading problems.

### <a name="hoerner"></a>"Fluid-Dynamic Life" and "Fluid-Dynamic Drag" by Sighard F. Hoerner
Following World War 2, the aerodynamics field exploded with pioneers and researchers like Dr. Hoerner leading the way. In the same way that Professor Bruhn's text is go-to reference for the analysis of flight vehicle structures, Hoerner's books are absolutely fundamental for aerodynamic analysis of all kinds.

### <a name="ntrs"></a>[NASA Technical Reports Server (NTRS)](https://ntrs.nasa.gov/search.jsp)
NTRS contains a vast wealth of information dating back to the early days of NASA, when they were known as the National Advisory Committee for Aeronautics (NACA) from 1915 to 1958. Major topics of interest include both aeronautics and aerospace research, such as NACA airfoil test data; aerodynamic test data; flight vehicle design manuals; and design manuals on rocket staging, propellants, etc.

Since the amount of data is so vast, the recommended usage for NTRS is to have a very specific query on a design or analysis problem — there's a decent chance that someone at NASA has already done the legwork for you. An example of a good query is `buckling thin shell` and `double slotted flap`. I also suggest filtering the `Document Type` to only contain "Technical Reports", which will only show NASA design manuals and technical memos.

Documents of interest on various topics:

* [NASA-SP-125: Design of Liquid Propellant Rocket Engines, Second Edition by D.H. Huang & D.K. Huzel](https://ntrs.nasa.gov/search.jsp?R=19710019929)
* [NASA-RP-1228: Fastener Design Manual by Richard T. Barrett](https://ntrs.nasa.gov/search.jsp?R=19900009424)
* [NASA-SP-8007: Buckling of thin-walled circular cylinders by Peterson-Seide-Weingarten](https://ntrs.nasa.gov/search.jsp?R=19690013955)

---

## <a name="python-references"></a>Python References

This section assumes that you have zero programming knowledge. Your goal here is to go through these references in order, and get from your first `Hello world!` program to what Chris Moffitt calls the ["plateau of productivity"](http://pbpython.com/plateau-of-productivity.html).

Many people who start coding for the first time get stuck in the "trough of disillusionment" stage of learning, and struggle to break out of it. I pushed a boulder up this same hill many times, only to fall back into the trough and give up for a while. But after a bit of a learning curve, I can attest that it has certainly been worth all the effort, not only in time saved, but also in the sense of accomplishment.

### <a name="why-python"></a>Why Python?
* It's easy to learn and a great first coding language
* You can go from learning to productive within a few weeks
* It's a mature language with many libraries and tons of documentation (Python 1.0 came out in 1994!)
* It has many applications, from basic scripting to data analysis to machine learning

### <a name="beginner-novice"></a>Beginner-Novice
Whether you're learning to code for the first time or simply adding Python to your list of languages, these resources will get you up and running quickly.

#### <a name="learning-python-for-the-first-time"></a>Learning Python for the First Time
There are five main resources recommended by the Python community, all of them free:

1. [Automate the Boring Stuff with Python](http://inventwithpython.com/#automate) by Al Sweigart
1. [Dive into Python 3](http://www.diveintopython3.net/) by Mark Pilgrim
1. [Think Python](http://greenteapress.com/wp/think-python-2e/) by Allen B. Downey
1. [Python 101](http://python101.pythonlibrary.org/index.html) ([ebook version here](https://leanpub.com/python_101)) by Michael Driscoll
1. [The Official Python Tutorial](https://docs.python.org/3/tutorial/index.html) by the Python Software Foundation

You only need to choose one and stick with it, but as we are all blessed with different minds, you'll want to try several to see which is more suited to your learning style. As my electrical engineering professor Keith Garfield wisely told me, *"Find a voice that speaks to you."*

All of them cover the basics of Python, but don't completely overlap in topics covered. The main difference is that 1 & 2 get you off the ground faster, letting you create practical programs very quickly, while 3-5 take longer to get through, but are more comprehensive and focus on helping you build a solid foundation in Python. It's completely fine to go with one of the faster resources and fill in the gaps later when you can accommodate it.

I like "Automate the Boring Stuff with Python" the best, which took me about 50 hours (and numerous tries) to get through. At some point you'll start to get the itch to write a 'real' program. That's perfectly normal, and I encourage you to start applying what you've learned by coding small personal projects. Finding problems and solving them with Python is the best way to get productive fast, rather than spending all your time reading and watching videos.

The only resource I recommend avoiding is "Learn Python the Hard Way" by Zed Shaw, mainly because it's outdated.

#### <a name="code-like-a-pythonista"></a>[Code Like a Pythonista: Idiomatic Python](http://python.net/~goodger/projects/pycon/2007/idiomatic/handout.html)
As you learn Python, you'll start to understand why styling and whitespace are important. David Goodger's "Code Like a Pythonista" and similarly [PEP8](https://www.python.org/dev/peps/pep-0008/) are important companions to have so that you can learn to write nice, readable code as you get better at Python. While you can afford to skip over some bits of Python as a language to learn at a later time, you can never afford to write crappy code because it is the antithesis to saving time.

As MIT's [SICP](https://mitpress.mit.edu/sicp/full-text/book/book-Z-H-7.html) wisely stated:

> \[...] a computer language is not just a way of getting a computer to perform operations but rather \[...] it is a novel formal medium for expressing ideas about methodology. Thus, programs must be written for people to read, and only incidentally for machines to execute.

Or as [The Zen of Python](https://www.python.org/dev/peps/pep-0020/) simply says: __Readability counts.__

#### <a name="pbpython"></a>[Practical Business Python](http://pbpython.com/)
PB Python is a monthly-ish blog by Chris Moffitt ([@chris1610](https://github.com/chris1610/pbpython)) that covers applications for Python that can be used in an everyday business setting. This is probably the best resource around for accelerating your Python skills from writing dinky Python exercise programs to programs that will save you time. It's also a fantastic resource for getting started with `pandas` (Python Data Analysis Library) for the first time, and bridging the gap between Excel and Python.

My recommended approach is to head into the [PB Python Archive](http://pbpython.com/archives.html) and start with the first article from 5 October 2014, ["Using Sets for Data Analysis"](http://pbpython.com/data-analysis-with-sets.html). As you move forward, go through each article in chronological order. Chris does a fantastic job of building upon his previous articles!

**Note:** For planning purposes, each PBpy exercise can take 1-2 hours to get through, depending on the topic and your skill level.

#### <a name="learning-python"></a>"Learning Python, 5th Ed." by Mark Lutz
This text is perhaps the most comprehensive resource for learning how Python works, and covers some advanced topics that aren't in any of the [Learning Python for the First Time](#learning-python) resources, such as interfacing Python with C/C++. This is of particular interest for engineers that work with embedded systems that require C/C++, or anyone that desires the computational power of C/C++ while keeping the ease of development in Python.

Since this book is an absolute behemoth of over 1,600 pages, I recommend it mainly as a companion reference for looking up concepts & examples that aren't explained thoroughly by any of the free resources. For even more exercises, Mark Lutz made his [live course materials](http://learning-python.com/training) available for free.

#### <a name="python-in-a-nutshell"></a>"Python in a Nutshell" by Martelli-Ravenscroft-Holden

---

### <a name="intermediate-advanced"></a>Intermediate-Advanced
By the time you've completed some medium to large programming projects on your own, you may need some more resources to reach the next skill level. These books will help correct some of the bad habits you've undoubtedly picked up while learning Python, and fill in any knowledge gaps while also delving into more advanced programming methods.

Note that unlike the Beginner resources, each of these textbooks has something different to offer.

#### <a name="fluent-python"></a>"Fluent Python: Clear, Concise, and Effective Programming" by Luciano Ramalho

#### <a name="effective-python"></a>"Effective Python: 59 Specific Ways to Write Better Python" by Brett Slatkin

[From the author of "Effective Python" on the differences from "Python Cookbook"](https://www.reddit.com/r/Python/comments/31zjy5/book_effective_python_vs_python_cookbook_which/cq6nl66/):

> Author of Effective Python here. I think they're very different books! David Beazley is awesome and a wonderful educator. He's always the best speaker at PyCon. I'd say: the _Cookbook_ is a powerful and thorough reference, the _Effective_ books are short and scenario driven.

#### <a name="python-cookbook"></a>"Python Cookbook" by David Beazley and Brian K. Jones

#### <a name="hackers-guide-to-python"></a>"The Hacker's Guide to Python" by Julien Danjou

---
