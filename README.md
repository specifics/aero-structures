# <a name="top"></a>aero-structures
Resources for analyzing aircraft structures for aerospace engineers.

# <a name="scope"></a>Scope
This resource page covers many topics that are needed to analyze aircraft structures using classical methods developed from prominent engineering minds such as Elmer F. Bruhn, Michael Niu, Warren Young (aka Raymond J. Roark), and Sighard F. Hoerner. FEA methods are not covered.

Additionally, this page also covers ways to port these methods into Python 3, allowing engineers become more effective at their job by rolling their own code to effectively interface with other engineers in a professional environment.

Ultimately, these resources should:
* Be a quick reference for non-FEA structural analysis methods used in the aerospace industry
* Help you [save time](https://xkcd.com/1205/) by automating & optimizing routine analysis in Python
* (TBD)

# <a name="rationale"></a>Rationale
A frequent problem engineers run into is having to effectively communicate analysis & findings to their colleagues, managers, and clients. The problem occurs when engineers fail to document their process in a meaningful and accessible way. As programmers quickly learn, the person most confused by reading your code is your future self, especially when you neglect to include comments and docstrings. This page is a first step in documenting my most frequently used analysis tools, and hopefully serve as a template for you to do the same.

Another, more aerospace-specific problem exists for professional engineers and students. While there are many resources for aerospace engineering, much of it is scattered about disparate places around the net (e.g. [NASA NTRS](https://ntrs.nasa.gov/search.jsp), countless threads on [Eng-Tips](http://www.eng-tips.com/)) and around the world. The aerospace industry in particular has a lot of "tribal" knowledge that becomes lost when veteran engineers, mechanics, and fabricators retire or pass away without disseminating their decades of experience and knowledge to the next generation. There's simply no replacement for this knowledge, and very little of it makes it into modern aerospace texts, let alone the lecture hall.

For students, this is problematic when trying to attain the requisite knowledge to enter a very limited and competitive job market. Some of these resources will address the *"Why didn't I learn this in school?"* moments that new engineers will almost certainly encounter during their formative years. Hopefully these resources will accelerate that learning process and save young engineers from committing serious but preventable mistakes.

---

# <a name="toc"></a>Table of Contents
<details open><summary><sup>Hide</sup>/<sub>Show</sub></summary><br/>



[⇪ Top](#toc)
</details>

---

<details open><summary><sup>Hide</sup>/<sub>Show</sub></summary><br/>

## Symbols & Abbreviations

* AN: Army-Navy Standard
* FEA: Finite Element Analysis
* MIL: Military; see MS
* MS: Military Standard

</details>

## Universal References
As mentioned in the Scope section, these references are truly universal in that they are frequently used by aerospace stress engineers to conduct basic & advanced analysis. While FEA is a powerful analysis tool, it comes with a lot of costs and overhead that isn't practical or necessary for a lot of engineering problems. In many cases a problem can be solved using a straightforward analysis process out of these texts, and if necessary, automated using a Python script. A common saying in engineering is, *"Someone a lot smarter than me figured this out 50 years ago."* -- which is really just another way of saying *"Don't re-invent the wheel."*

**Students beware:** Most of these are not suitable textbooks for learning course material.

### Metallic Materials Properties Development and Standardization (MMPDS)
MMPDS is a database of statistically-verified strength data for common aerospace materials and fasteners, which serves as the basis for design manuals in nearly every aerospace company. While a new version of MMPDS gets released every few years, there's nothing wrong with using an older version. MMPDS-01 is available for free from the [National Technical Reports Library](https://ntrl.ntis.gov/NTRL/dashboard/searchResults/titleDetail/PB2003106632.xhtml) (U.S. Dept. of Commerce), but in case it ever isn't, a copy will remain available [here on this github page.](/reference/MMPDS-01.pdf)

**Note:** For all intents and purposes, MMPDS supercedes MIL Handbook. MMPDS-01 contains data equivalent to MIL-HDBK-5J.

SHA256 hash for MMPDS-01: `4e252754c126d71d877222b80dba0a0641acc672e1052a7844058ada009118de`

### "Analysis and Design of Airplane Structures" by Elmer F. Bruhn
Considered by many to be 'the Bible' of flight vehicle analysis, Professor Bruhn detailed empirical design methods and calculation processes for aircraft structures that were used for practically every aircraft design from the 1940s and onward, until the advent of FEA and computer-driven numerical methods in the mid-1970s. 

This book no longer appears to be published, so if you find a copy, buy it.

### "Airframe Structural Design: Practical Design Information and Data on Aircraft Structures" by Michael Niu
Niu was the Senior R&D Engineer at Lockheed Martin and Stress Engineer at Boeing Co. during the development of the 727 and 747. With over 30 years of experience, Niu puts nearly every detail design consideration required for initial sizing and 
