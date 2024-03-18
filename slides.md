# Agenda

- Introduction
- History Lesson
- Where we are
- Recent Events
- Call to Action
- Q & A


# About me

- Vulnerability research and exploit development career

- Most recently Sr. Security Engineer at Amazon Lab126

- Bootstrapping a security startup

- Developing strategic Rust implementations

- Previously:
<div class="about-logos">
 <img height=120px src="/lib/img/amsec-trans-w.png" />
 <img height=120px src="/lib/img/sflogo.png" />
 <img height=120px src="/lib/img/ahh.png" />
 <img height=120px src="/lib/img/msf.svg" />
 <img height=40px src="/lib/img/idef.png" />
</div>


## Motivations

1. Improve global security maximally through computer science and engineering.
2. Raise awareness to build cross-industry momentum and standardization.
3. Evangelize safer development methods and technologies


## Disclaimer

I feel vastly underqualified to cover this topic. This presentation is
my best effort to show the state of the art and share my experiences,
thoughts, and opinions.

Please take time to think about the content and formulate your own ideas/response.


## Trust and Guarantee

<div class="footnote">
1. <a href="https://arxiv.org/html/2402.01944v1">SoK: Guarantees in Software Security</a>
</div>

- Trust
  - "belief in relability, truth, ability or strength of"
  - in this talk, of the security of software humans build
- Guarantee
  - "a formal promise or assurance that certain conditions will be fulfilled"
  - SoK Paper by Marcel Bohme is a must read.

Both of these concepts are crucial to understanding software security.

<aside class="notes">
Think: Do you trust your software's security?<br />
Think: What guarantees are provided by your tools?<br />
The paper by Marcel in the footnote is a must read -- for developers and security alike.<br />
Trust is our goal, and guarantees set a baseline.
</aside>

---

<!-- .slide: class="ctitle" -->
# History Lesson
<div class="ctitle-line"></div>

## How did we get here?


# My Journey

* Mischievious since birth
* Programming since age 11
* Internet user since age 13
* Learned C programming in 1995
* Studied Math + CS in university


# My Journey

<div class="footnote">
1. <a href="https://packetstormsecurity.com/files/25349/formatstring-1.2.tar.gz.html">Exploiting Format String Vulnerabilities by scut</a>
</div>

* Modified client based on on ircII
  * Abandoned! Do not use! (FreeBSD ports??)
* Found format string bugs after reading Teso paper.
* Realized securing software written in C is very hard.
* Decided to pursue security as a career path.

<div class="ninja">
 <img src="/lib/img/ninja1.png" />
</div>

<aside class="notes">
Around 2001, the security industry was just taking off. I was developing a customized version of ircII along with Kraig Amador.<br />
I was researching security and learning to audit C code.<br />
I looked at our code and discovered several issues, including bugs that were exploitable by other irc users.<br />
Fixed the bugs, but also came to the realization that developing secure software in C is very hard.<br />
As I learned more, I quickly lost hope in shipping code that others relied on.
</aside>


# Microsoft's Example

<div class="footnote">
1. <a href="https://www.nbcnews.com/id/wbna4641234">Bill Gates sends security memo to customers</a><br />
2. <a href="https://www.microsoft.com/en-us/security/blog/2022/01/21/celebrating-20-years-of-trustworthy-computing/">Celebrating 20 Years of Trustworthy Computing</a>
</div> 

Microsoft had big security problems in early 2000's.
 - Windows was around 96% market share
 - Several worms attacking various bugs
 - Bill Gates took action
 - Led to many industry improvements, by following their lead


## RCE in Microsoft ATL

<div class="footnote">
1. <a href="https://learn.microsoft.com/en-us/security-updates/securitybulletins/2009/ms09-037">MS09-037: Microsoft Active Template Library (ATL) RCE</a><br />
2. <a href="https://learn.microsoft.com/en-us/security-updates/securitybulletins/2009/ms09-060">MS09-060: Microsoft ATL ActiveX Controls for Microsoft Office RCE</a>
</div>

<div class="atlcve">
<br />
CVE-2009-2493
</div>

- Research by Ryan Smith
- Estimated industry cost: **10-100 million**
- Incorrect characters in source code: **one**

<aside class="notes">
Back in 2009, Ryan Smith found an RCE bug in an ActiveX.<br />
Further investigation revealed that it likely stemmed from a stray '&' in the ATL header file in Microsoft's code.<br />
It was reported and fixed, but actually fixing it depend on every person that used this header recompiling their code.<br />
Estimated industry cost was in the 10-100 million range.<br />
We eventually got confirmation from a Microsoft employee that it was indeed caused by a stray ampersand.<br />
So one extra byte in a header file caused such a huge fallout?
</aside>


# Undefined Behavior

<div class="footnote">
1. <a href="https://en.wikipedia.org/wiki/Undefined_behavior">Wikipedia on Undefined Behavior</a><br />
2. <a href="https://gist.github.com/Earnestly/7c903f481ff9d29a3dd1">C99 List of Undefined Behavior</a><br />
3. <a href="https://www.youtube.com/watch?v=k9N8OrhrSZw">What every programmer should know and fear</a><br />
4. <a href="https://www.safetyresearch.net/toyota-unintended-acceleration-and-the-big-bowl-of-spaghetti-code/">Toyota Unintended Acceleration</a>
</div>

- Intentional ambiguity in the C language specification
  - The C99 specification contains <b>193</b> mentions of UB.
    - Do newer standards have more or less?
  - Leaves compiler engineers without requirements

- Birthed many security issues, bugs, and even loss of human life &#x1f620;

- Ambiguity is the inverse of guarantee

<aside class="notes">
I went on learning about different types of bugs and bug classes.<br />
I learned to write exploits as a challenge to myself.<br />
Eventually I learned what appeared to be the cause for all this trouble -- undefined behavior.
</aside>


## Assumptions, Reality, and Evolution

<div class="footnote">
1. <a href="https://lwn.net/Articles/820969/">A remote code execution vulnerability in qmail (LWN)</a>
</div>

The reality is that most humans make assumptions when developing software.

For example, DJB assumed that type sizes wouldn't change in the future.

This eventually led to a security issue in his qmail software when 64-bit started to emerge.

The reality is that most developers make far more assumptions.

---

<!-- .slide: class="ctitle" -->
# Where we are
<div class="ctitle-line"></div>

## Where does all that lead?


## We Are In a Bad Place<sup>tm</sup>

<div class="footnote">NOTE: Please forgive the impending rant...</div>

Problems:
- People problems...
- Security industry fails
- Government fails
- Software vendor fails


## People Problems

- Insufficient developer and security education
  - Many developers don't know security
  - Many security people don't know development

We have a lot to learn from each other

Open your minds and seek to learn!


## Security Industry Fails

<div class="footnote">NOTE: We should celebrate exceptions and seek to learn from them.</div>

- Security products shipping with security bugs
- Lack of scientific approach / rigor
  - Tons of private reporting and silent fixes
- Assessments time-boxed and point-in-time
  - Review scope is too large to deliver quality
- Unwilling to jump in to fix the code
- Not enough qualified practioners

I bet you can think of other things too!


## Government Fails

Lack of regulation on the software industry has led to forseeable failure.

Participation in zero-day markets removes many talented persons from the pool
of qualified security practitioners.

<aside class="notes">
Whether you know it or not, the US (and other) governments fund vulnerability research.<br />
This takes talented resources away from the pool of potential security industry practioners.
</aside>


## Software Vendor Fails

<div class="footnote">NOTE: We should celebrate exceptions and seek to learn from them.</div>

- Market incentives undermine security
  - Good, Fast, Cheap -- Pick two.
- No SDLC?
  - SDLC was born 20 years ago.
- C and C++ widely used, but error prone
- Ignore compiler warnings
- Ignore static analysis tool output
- Testing severely lacking
  - Fuzz much??


## All the safety is not enough

Bugs will still happen

- Command injection, SQL injection, XSS, all the injections
- Logic errors
- Authentication missing or poorly implemented
- Crypto fails
- ...and so on

**But memory safety issues are reportedly 70% of the problems that Microsoft and Google encounter and fix.**

---

<!-- .slide: class="ctitle" -->
# Recent Events
<div class="ctitle-line"></div>

## What happend in the past few years?


## All About Software Safety

<div class="footnote">
1. <a href="https://saaramar.github.io/memory_safety_blogpost_2022/">Survey of security mitigations and architectures, December 2022</a><br />
2. <a href="https://alexgaynor.net/2019/aug/12/introduction-to-memory-unsafety-for-vps-of-engineering/">Intro to Memory Unsafety for VPs</a><br />
3. <a href="https://yoric.github.io/post/safety-and-security/">About Safety, Security and yes, C++ and Rust</a>
</div>

Many things to think about:

- Temporal safety
- Spatial safety (bounds)
- Type safety
- Definite initialization
- Thread safety

Check out Saar Amar (Dec 2022) and David Teller (Feb 2023) writings.


# Government Activism

<div class="footnote">
1. <a href="https://media.defense.gov/2022/Nov/10/2003112742/-1/-1/0/CSI_SOFTWARE_MEMORY_SAFETY.PDF">NSA Paper on Memory Safety, Nov 2022</a><br />
2. <a href="https://www.whitehouse.gov/wp-content/uploads/2023/03/National-Cybersecurity-Strategy-2023.pdf">National Cybersecurity Strategy</a> (<a href="https://www.regulations.gov/docket/ONCD-2023-0002/comments">107 RFI comments</a>)<br />
3. <a href="https://www.cisa.gov/sites/default/files/2023-10/SecureByDesign_1025_508c.pdf">Secure By Design</a> (<a href="https://www.regulations.gov/docket/CISA-2023-0027/comments">83 RFI comments</a>)<br/>
4. <a href="https://www.whitehouse.gov/wp-content/uploads/2024/02/Final-ONCD-Technical-Report.pdf">Back to the Building Blocks</a>
</div>

Governments turning Memory Safety into a MEME!

Several papers and Federal Regsiter RFIs (and response comments on regulations.gov)

* 2022 - NSA Paper on Memory Safety
* 2023 - National Cybersecurity Strategy
* 2024 - Secure by Design (CISA + 13 other countries)
* 2024 - Back to the Building Blocks (ONCD)
  * Results from 2023 CFI


# Industry Activity

Even before the recent federal push, several vendors are leading by example.

* Google - Rust in Android, donated $1 mil
* Rust at Microsoft - win23k
* Apple investing in Swift in the kernel
* Rust in the Linux Kernel

Also, many startups are making smart choices.


# Hardware: MTE

<div class="footnote">
1. <a href="https://source.android.com/docs/security/test/memory-safety/arm-mte">Arm Memory Tagging Extension AOSP Docs</a><br />
2. <a href="https://dustri.org/mte/">Collection of MTE related crashes</a>
</div>

Memory Tagging Extension

64-bit ARM spatial/temporal safety enforcement
* Unfortuantely, probalistic (only N-tags)

Present in Google Pixel 8 and 8 Pro and hopefully others
- Disabled by default in Pixel OS, but easy to enable
- Enabled by default in [GrapheneOS](https://grapheneos.org/)
- Exposes poor software quality!


# Hardware: CHERI

<div class="footnote">
1. <a href="https://www.cl.cam.ac.uk/research/security/ctsrd/cheri/">https://www.cl.cam.ac.uk/research/security/ctsrd/cheri/</a><br />
2. <a href="https://www.morello-project.org/">https://www.morello-project.org/</a>
</div>

Capability Hardware Enhanced RISC Instructions (CHERI)
 - "joint research project of SRI International and the University of Cambridge to revisit fundamental design choices in hardware and software to dramatically improve system security"

Capabilities are bounded pointers / cannot be forged

Expect silicon in fall 2024 (fingers crossed)

For now: Morello project

<aside class="notes">
CHERI represents a paradigm shift in computing
</aside>


# OpenSSF

<div class="footnote">1. <a href="https://openssf.org/">https://openssf.org/</a></div>

Open Source Security Foundation
 - "seeks to make it easier to sustainably secure the development, maintenance, and consumption of the open source software (OSS) we all depend on."

Funded by the Linux Foundation

Many efforts: Training, Scorecard, Alpha-Omega, Memory Safety WG, etc


# C++ Community

<div class="footnote">
1. <a href="https://github.com/bjarneStroustrup/profiles">Bjarne's Profiles repo on GitHub</a><br />
2. <a href="https://github.com/hsutter/cppfront">Herb's CPPFront repo on GitHub</a><br />
3. <a href="https://herbsutter.com/2024/03/11/safety-in-context/">C++ safety, in context by Herb</a>
</div>

The C++ community is taking safety seriously, but unclear what will be
standardized and when.

Maybe C++26?

* Bjarne Stroustrup - C++ Safety Profiles etc
* Herb Sutter - cppfront, ISO C++ Chair, blogging
* Sean Baxter ([@seanbax](https://twitter.com/seanbax)) - "Memory-safe C++"
  - Engage with him on X/Twitter


# Defining Undefined Behavior

<div class="footnote">
1. <a href="https://www.open-std.org/jtc1/sc22/wg21/docs/papers/2019/p1705r1.html">P1705R1: Enumerating Core Undefined Behavior in C++</a><br />
2. <a href="https://community.intel.com/t5/Blogs/Tech-Innovation/Tools/Why-do-we-need-a-Undefined-Behavior-Annex-for-the-C-standard/post/1574397">Why do we need a Undefined Behavior Annex for the C++ standard?</a>
</div>

Shafik Yaghmour (Intel) is working to drive change around "undefined behavior".

<a href="https://wg21.link/P1705">https://wg21.link/P1705</a>

I emailed him with encouragement, but no response :-/

IDEA: Maybe we should attempt to define the behavior based on empirical observations?


# Other Interesting Stuff - Fil-C

<div class="footnote">
1. <a href="https://github.com/pizlonator/llvm-project-deluge">Fil-C on GitHub</a>
</div>

Fil-C is a modified compiler to produce memory safe programs from C source code.

"The Fil-C Manifesto: Garbage In, Memory Safety Out!"

by Filip Jerzy Pizlo ([@filpizlo](https://twitter.com/filpizlo))

<div class="filc">
  <img src="/lib/img/chisnall-on-fil-c.png">
</div>

---

<!-- .slide: class="ctitle" -->
# Call to Action
<div class="ctitle-line"></div>

## What can we do?


## Hot Buzzwords

Shift left
 - Move testing earlier in the process
 - Developers lose context over time -- tighter feedback loops are more efficient

DevSecOps
 - Core idea is integrating security processes within development pipelines
 - To block or not to block? That is the question


## Milestones in a SDLC

1. Inception of the idea to develop something
2. Creation of a design
3. Threat modeling / identifying mitigations to threats
- Understand the attack surface and classify risk with hypothetical CVSS
- This is a good time to design counter measures and feature flags
4. Implementation
5. Testing
6. Verification

And the cycle continues... Perhaps need a graphic?


## Other beneficial practices

1. Creating guidelines / coding standards and adhering to them.
2. Well executed code reviews by qualified colleages
3. Periodically revisiting the software to assess environmental drift
4. Inviting open participation to review - open source / bug bounties / etc


## Programming Language Choice

Often viewed as a religious discussion.

- you can create safe and secure code in any language, but the amount of effort it will require differs
  - C
  - C++
  - Rust
  - Go
  - Python
  - other?


# Thoughts on C

- A language for computer wizards
  - Literal minefield of inconsistency
  - Immense burden put on the developer
- Little to no improvements for a long, long time
  - Why not improve string APIs??


# Thoughts on C++

- Many improvements but often with new footguns
  - Example: move semantics in C++11
- Backward compatibility is a primary goal
  - Leads to "C/C++" code
  - Guarantees require breaking changes
- Adoption rate is *VERY* slow
  - Most C++ teams use C++17 at best


# About CWE

<div class="footnote">
1. <a href="https://cwe.mitre.org/about/index.html">CWE About Page - MITRE</a><br />
</div>

Common Weaknesses Enumeration

- CVEs lesser-known little brother
- Huge catalog of ways developers have introduced security issues into software
- Includes many real-world code excerpts
- Supports multiple languages and views
- <b>Should be studied by every developer</b>
- See also Top 25 etc


## Good, Fast, Cheap

Not enough people?
  - Take an apprentice!
 - lack of rigor in security testing.
   - what was tested? who tested it? what did they find?
   - what WASNT tested?

Triangle?
Which one?
Is a balance really unobtanium?
Is releasing a poor quality product really in your company's best interest?

Evidence shows that better quality leads to better efficiency (TODO: source)


## SDLC

Secure Development Life Cycle


## formal verification tools

 - coq
 - frama-c
 - cbmc
 - kani


## static analyzers

 - noisy much?


## fuzzing

 - pretty good bang for the buck, but requires knowledge of the code
 - applicable to all programming languages


## What else can we do?

Computer security history class? How about that?
This would be a good one for engineers to need to take. It doesn't have to be at every university either. It can be a collaboration between multiple or one that gets accredited by professionals and other professors


# Memory Safety

I recommend modern langauges unless absolutely necessary


# Nah, Memory Safety Isn't for Us

* Sanitizers - UB, Address, Thread, etc.
* Extensive tests / Fuzz testing
* Feed failures back into security testing pipeline


# Call to Action

Let's get scientific!

Consider your projects as collections of experiments

Document them using Hypothesis / Experiment Design / Notes / Results format

Security assessment is specialized QA


# Call to Action

More configurable features flags

Some call them "andon cords"

All the big vendors have them, but we need more

And we need to allow consumers to toggle them


# More Transparency

Who audited what -- Exactly??
- This is currently tracked sometimes, but only indirectly (CVE credits etc)


## Takeaways

Transparency
Disablement features / Andon Cords
Security assessment is specialized QA


## Conclusion

Developing secure software is hard work.
Many businesses are not willing to invest the time and effort to produce robust software.
Modern tools and techniques can help to reduce the burden.

---

<!-- .slide: class="discussion" -->
# Thanks for your time!

## Any questions or comments?

Feel free to reach out later:
<div class="contactinfo">
Joshua J. Drake<br />
jduck @ Twitter/Discord/Mastadon/etc<br />
</div>

---

# About these slides

Slides were created in <a href="https://revealjs.com/markdown/">markdown with nreveal.js</a>

You can export by printing the <a href="/?print-pdf">PDF</a>

---

<div class="fin">the real end. really.</div>

