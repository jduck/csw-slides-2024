# Agenda

- Introduction
- History Lesson
- Where we are
- Ongoing Efforts
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
my best effort to show the state of the art and share my experiences/opinions.


## Trust and Guarantee

<div class="footnote">
1. <a href="https://arxiv.org/html/2402.01944v1">SoK: Guarantees in Software Security</a>
</div>

- Trust
  - "belief in relability, truth, ability or strength of"
  - in this case, of the security of software humans build
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

<div class="ninja">
 <img src="/lib/img/ninja1.png" />
</div>

* Modified client based on on ircII
  * Abandoned! Do not use! (FreeBSD ports??)
* Found format string bugs after reading Teso paper.
* Realized securing software written in C is very hard.
* Decided to pursue security as a career path.

<aside class="notes">
Around 2001, the security industry was just taking off. I was developing a customized version of ircII along with Kraig Amador.<br />
I was researching security and learning to audit C code.<br />
I looked at our code and discovered several issues, including bugs that were exploitable by other irc users.<br />
Fixed the bugs, but also came to the realization that developing secure software in C is very hard.<br />
As I learned more, I quickly lost hope in shipping code that others relied on.
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


## About Safety

<div class="footnote">
1. <a href="https://saaramar.github.io/memory_safety_blogpost_2022/">Survey of security mitigations and architectures, December 2022</a><br />
2. <a href="https://alexgaynor.net/2019/aug/12/introduction-to-memory-unsafety-for-vps-of-engineering/">Intro to Memory Unsafety for VPs</a><br />
</div>

Refer to Saar Amaar / David Teller posts on the subject

NOTE: People have died because of bad software -- Integer Overflow in Toyota code leads to stuck accelerator (need sources)

How much time and money has been spent on playing whack-a-mole?

- Bounds safety
  - Rust bounds checking
  - Temporal safety
    - Rust lifetimes
    - Thread safety
      - Send/Sync traits


## About Correctness

What does it mean to say a program is correct?


## Assumptions and Reality

The reality is that we all make assumptions when developing software.
For example, DJB assumed that type sizes wouldn't change in the future.
The reality is that most developers make far more assumptions.


## Story: RCE in Microsoft COM

Ryan Smith found a bug that allowed RCE in the browser.
Further investigation revealed that it likely stemmed from a stray '&' in a header file in Microsoft's code. 
It was reported and fixed, but actually fixing it depend on every person that used this header recompiling their code. Estimated industry cost was in the 10-100 million range.
We eventually got confirmation from a Microsoft employee that it was indeed caused by that stray ampersand.
So one extra byte in a header file caused such a huge fallout?


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


# Summary

1. The tools developers rely on have let us down.
2. The education system has not adapted. -- with sources

---

<!-- .slide: class="ctitle" -->
# Where we are
<div class="ctitle-line"></div>

## Where does all that lead?


## We Are In a Bad Place<sup>tm</sup>

<div class="footnote">NOTE: We should celebrate exceptions and seek to learn from them.</div>

Problems:
- Insufficient developer security education
- Not enough qualified practioners
- Market incentives undermine security
- C and C++ widely used, but poorly supported
- Scope is too large to deliver quality
- Security often time-boxed and point-in-time
- Testing is severely lacking
- and more!


## TODO - slides for state of things

DevSecOps?

Shift left?


## Failures everywhere

From market incentives to ethical dilemmas, it's no quesetions that the failures are many -- too many to discuss all of them. 

Failures of security industry
 - delivery of products that are fallible
 - over promise and under delivery (pentest scopes are huge and rarely fully completed)
 - lack of rigor in security testing.
   - what was tested? who tested it? what did they find?
   - what WASNT tested?
 - overly focused on showing one specific example of failure

Failures of government
 - lack of regulation and enforcement leads companies free to deprioritize security
 - participation in zero-day markets removes a large part of qualified workforce from the market

Failures of software manufacturers
 - overly focused on speed to market
 - overly focused on minimizing costs and maximizing profits
 - lack of understanding of the core problems (CWE awareness)
 - deciding not to participate in the global security community
 - not giving security/QA the concern and respect it needs
 - leadership sends correct message, but does not follow through
   - this message is twisted and even ignored as it flows through an organization
 - even with a great SDLC design, does not execute it properly


## All the safety is not enough

1. Bugs will still happen
   - Command injection, SQL injection, XSS, all the injections
   - Logic errors
   - Authentication missing or poorly implemented
   - Crypto fails
   - More?


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


## Programming Language choices

- you can create safe and secure code in any language, but the amount of effort it will require differs
  - C
  - C++
  - Rust
  - Go
  - Python
  - other?


# Thoughts on C

TODO


# Thoughts on C++

TODO

---

<!-- .slide: class="ctitle" -->
# Ongoing Efforts
<div class="ctitle-line"></div>

## What just happened / is happening?


# Ongoing - Government Activism

<div class="footnote">
1. <a href="https://www.whitehouse.gov/wp-content/uploads/2023/03/National-Cybersecurity-Strategy-2023.pdf">National Cybersecurity Strategy</a> (<a href="https://www.regulations.gov/docket/ONCD-2023-0002/comments">107 RFI comments</a>)<br />
1. <a href="https://www.cisa.gov/sites/default/files/2023-10/SecureByDesign_1025_508c.pdf">Secure By Design</a> (<a href="https://www.regulations.gov/docket/CISA-2023-0027/comments">83 RFI comments</a>)<br/>
2. <a href="https://www.whitehouse.gov/wp-content/uploads/2024/02/Final-ONCD-Technical-Report.pdf">Back to the Building Blocks</a>
</div>

Several Federal Regsiter RFIs and papers

Extensive comments available on regulations.gov

* 2023 - National Cybersecurity Strategy
* 2024 - Secure by Design (CISA + 13 other countries)
  1. Take ownership of customer security outcomes
  2. Embrace radical transparency and accountablity
  3. Build org structure/leadership to achieve goals
* 2024 - Back to the Building Blocks (ONCD)
  * Results from 2023 CFI


# Ongoing - Industry Response

* Google: pushing memory safety, leading by example


# Ongoing - Hardware: MTE

Memory Tagging Extension

64-bit ARM spatial/temporal safety enforcement
* Unfortuantely, probalistic (only N-tags)

Present in Google Pixel 8 and 8 Pro and hopefully others

Enabled by default in [GrapheneOS](https://grapheneos.org/)


# Ongoing - Hardware: CHERI

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


# Ongoing - OpenSSF

<div class="footnote">1. <a href="https://openssf.org/">https://openssf.org/</a></div>

Open Source Security Foundation
 - "seeks to make it easier to sustainably secure the development, maintenance, and consumption of the open source software (OSS) we all depend on."

Funded by the Linux Foundation


# Ongoing - Defining Undefined Behavior

https://www.open-std.org/jtc1/sc22/wg21/docs/papers/2019/p1705r1.html
http://wg21.link/P1705
Enumerating Core Undefined Behavior in C++

- TODO: Intel guy work (emailed him, no response)
- Shafik Yaghmour (Apple)


# Ongoing - Other Interesting Stuff

* Sean Baxter ([@seanbax](https://twitter.com/seanbax)) - "Memory-safe C++"
* Filip Jerzy Pizlo ([@filpizlo](https://twitter.com/filpizlo)) - [Fil-C](https://github.com/pizlonator/llvm-project-deluge/blob/deluge/Manifesto.md) 


# TODO - more slides

---

<!-- .slide: class="ctitle" -->
# Call to Action
<div class="ctitle-line"></div>

## What can we do?


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

