## Agenda

- Introduction
- History Lesson
- Where we are
- Recent Events
- Call to Action
- Conclusions
- Q & A


## About me

- Vulnerability research and exploit development career
- Most recently Sr. Security Engineer at Amazon Lab126
- Bootstrapping a security startup
- Developing strategic Rust implementations

Previously:
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

This presentation is my best effort to show the state of the art and share my
experiences, thoughts, and opinions.

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


## My Journey

* Mischievious since birth
* Programming since age 11
* Internet user since age 13
* Learned C programming in 1995
* Studied Math + CS in university


## My Journey

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


## Microsoft's Example

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


## Undefined Behavior

<div class="footnote">
1. <a href="https://gist.github.com/Earnestly/7c903f481ff9d29a3dd1">C99 List of Undefined Behavior</a><br />
2. <a href="https://www.youtube.com/watch?v=k9N8OrhrSZw">What every programmer should know and fear</a><br />
3. <a href="https://www.safetyresearch.net/toyota-unintended-acceleration-and-the-big-bowl-of-spaghetti-code/">Toyota Unintended Acceleration</a>
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
Eventually I learned what appeared to be the cause for all this trouble -- undefined behavior.<br />
IMHO, this is the ultimate technical debt in software development.
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

Potential solutions coming later in the talk


## People Problems

- Perceived staffing crisis
  - Not enough qualified practioners
- Insufficient developer and security education
  - Many developers don't know security
  - Many security people don't know development

We have a lot to learn from each other

Open your minds and seek to learn!


## Security Industry Fails

<div class="footnote">NOTE: We should celebrate exceptions and seek to learn from them.</div>

- Security products shipping with trivial security bugs
- Lack of scientific approach / rigor
  - Tons of private reporting and silent fixes
  - Assessments time-boxed and point-in-time
  - Review scope is too large to deliver quality
- Unwilling to jump in to fix the code

I bet you can think of other things too!

<aside class="notes">
- Who tested what?
</aside>


## Government Fails

Lack of regulation on the software industry has led to forseeable failures.

Zero-day markets removes many talented persons from the pool
of qualified security practitioners.

<aside class="notes">
Whether you know it or not, the US (and other) governments fund vulnerability research.<br />
This takes talented resources away from the pool of potential security industry practioners.<br />
When I left Amazon, I had 6 different VR firms reach out to me.<br />
Only one non-VR firm reached out.
</aside>


## Software Vendor Fails

<div class="footnote">NOTE: We should celebrate exceptions and seek to learn from them.</div>

- Market incentives undermine security
  - Good, Fast, Cheap -- Pick two.
- No Secure SDLC?
  - Microsoft SDL was born 20 years ago.
- C and C++ widely used, but error prone
- Ignore compiler warnings
- Ignore static analysis tool output
- Testing severely lacking
  - Fuzz much??

<aside class="notes">
Is releasing a poor quality product really in your company's best interest?<br />
Surely there's more to complain about here, but I digress.
</aside>

---

<!-- .slide: class="ctitle" -->
# Recent Events
<div class="ctitle-line"></div>

## What's going on?


## All About Software Safety

<div class="footnote">
1. <a href="https://saaramar.github.io/memory_safety_blogpost_2022/">Survey of security mitigations and architectures, December 2022</a><br />
2. <a href="https://alexgaynor.net/2019/aug/12/introduction-to-memory-unsafety-for-vps-of-engineering/">Intro to Memory Unsafety for VPs</a><br />
3. <a href="https://yoric.github.io/post/safety-and-security/">About Safety, Security and yes, C++ and Rust</a>
</div>

People are getting serious about "safety" in coding.

- Temporal safety
- Spatial safety (bounds)
- Type safety
- Definite initialization
- Thread safety

Check out Saar Amar (Dec 2022) and David Teller (Feb 2023) writings.


## Government Activism

<div class="footnote">
1. <a href="https://media.defense.gov/2022/Nov/10/2003112742/-1/-1/0/CSI_SOFTWARE_MEMORY_SAFETY.PDF">NSA Paper on Memory Safety, Nov 2022</a><br />
2. <a href="https://www.whitehouse.gov/wp-content/uploads/2023/03/National-Cybersecurity-Strategy-2023.pdf">National Cybersecurity Strategy</a> (<a href="https://www.regulations.gov/docket/ONCD-2023-0002/comments">107 RFI comments</a>)<br />
3. <a href="https://www.cisa.gov/sites/default/files/2023-10/SecureByDesign_1025_508c.pdf">Secure By Design</a> (<a href="https://www.regulations.gov/docket/CISA-2023-0027/comments">83 RFI comments</a>)
</div>

Governments turning Memory Safety into a MEME!

Several papers and Federal Regsiter RFIs (and response comments on regulations.gov)

* 2022 - NSA Paper on Memory Safety
* 2023 - National Cybersecurity Strategy + RFI
* 2023 - Secure by Design (CISA + 13 other countries)
* 2024 - Back to the Building Blocks (ONCD) [[LINK](https://www.whitehouse.gov/wp-content/uploads/2024/02/Final-ONCD-Technical-Report.pdf)]
  * Results from 2023 RFI

<aside class="notes">
Secure by Design presented at BlackHat USA 2023, then paper published early this year.
</aside>


## Industry Activity

Even before the recent federal push, several vendors are leading by example.

* Google - Rust in Android, donated $1 mil
* Rust at Microsoft - win23k
* Apple investing in Swift in the kernel
* Rust in the Linux Kernel

Also, many startups are making smart choices.


## Hardware: MTE

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


## Hardware: CHERI

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


## OpenSSF

<div class="footnote">1. <a href="https://openssf.org/">https://openssf.org/</a></div>

Open Source Security Foundation
 - "seeks to make it easier to sustainably secure the development, maintenance, and consumption of the open source software (OSS) we all depend on."

Funded by the Linux Foundation

Many efforts: Training, Scorecard, Alpha-Omega, Memory Safety WG, etc


## C++ Community

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

<aside class="notes">
I recommend following Sean on Twitter. He's doing really good work.<br />
Bjarne is mostly just defending his baby when given the chance. He means well.<br />
Herb is also doing work too, but not like Sean
</aside>


## Defining Undefined Behavior

<div class="footnote">
1. <a href="https://www.open-std.org/jtc1/sc22/wg21/docs/papers/2019/p1705r1.html">P1705R1: Enumerating Core Undefined Behavior in C++</a><br />
2. <a href="https://community.intel.com/t5/Blogs/Tech-Innovation/Tools/Why-do-we-need-a-Undefined-Behavior-Annex-for-the-C-standard/post/1574397">Why do we need a Undefined Behavior Annex for the C++ standard?</a>
</div>

Shafik Yaghmour (Intel) is working to drive change around "undefined behavior".

<a href="https://wg21.link/P1705">https://wg21.link/P1705</a>

I emailed him with encouragement, but no response :-/

&#x1f4a1; Document behavior in the spec based on empirical observations


## Other Interesting Stuff - Fil-C

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

You should know what these mean:
- Shift left
  - Move testing earlier in the process
  - Developers lose context over time -- tighter feedback loops are more efficient
- DevSecOps
  - Integrate security processes into development pipelines
  - To block or not to block? That is the question


## About CWE

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


## Implement SSDLC

<div class="footnote">
1. <a href="https://codesigningstore.com/secure-software-development-life-cycle-sdlc">Secure SDLC by CodeSigningStore (digicert)</a><br />
2. <a href="https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-218.pdf">NIST Secure Software Development Framework</a>
</div>

<div class="about-logos">
Secure Software Development Life Cycle
 <img src="/lib/img/ssdlc-process.png"><br />
<div style="font-size: 18pt">Image provided as an example only</div>
</div>


## Design Phase

**Early choices have long-lasting impact.**
- On security baselines
- On maintenance burden

Every feature is a potential attack surface.
- Design with response in mind

**Programming Language choices inherit technical debt**


## Programming Language Choice

Often viewed as a religious topic with many factors to consider. Some (subjective) properties:
<div class="pltab">

| lang    | perf.  | get compiled  | weaknesses | debug |
|---------|--------|---------------|------------|-------|
| C       | high   | medium        | high       | high  |
| C++     | high   | medium        | high       | high  |
| Rust    | high   | high          | low        | low   |
| Go      | high   | medium        | low        | low   |
| Python  | low    | n/a           | low        | low   |

</div>
I use and recommend modern langauges

<aside class="notes">
- You can create safe and secure code in any language, but the amount of effort required differs.<br />
- Older languages require a dev perfectly manage memory, lifetime, and so on.<br />
- Older languages have a tremendous number of potential foot guns.<br />
</aside>


## Thoughts on C

- A language for computer wizards
  - Literal minefield of inconsistency
  - Immense burden put on the developer
- Little to no improvements for a long, long time
  - Why not improve string APIs??


## Thoughts on C++

- Many improvements but often with new footguns
  - Example: move semantics in C++11
- Backward compatibility is a primary goal
  - Leads to "C/C++" code
  - Guarantees require breaking changes
- Adoption rate is *VERY* slow
  - Most C++ teams use C++17 at best


## Thoughts on Rust/Go

Ideal languages for the modern world.
- Benefit from decades of learning about software construction.
- Make it easier to write high quality code
- Comparable performance to C and C++
- Cost is mainly learning curve and memory
  - Computers have never been faster and memory has never been cheaper


# Obligatory Rust Slide

Bias warning: I &#x2764;&#xfe0f; Rust

- Safety focus
- Fast & Efficient
- Multi platform support
- Ecosystem
- **Empowering**

But this is not a talk on Rust.

<aside class="notes">
Rust uses a "safe by default" paradigm.<br />
"Unsafe" code must be explicitly annotated.<br />
Prevents or lessens the impact of traditional coding problems<br />
<br />
Keep an eye out for a blog post where I'll explain my love for Rust further.<br />
</aside>


## Threat Modeling 

<div class="footnote">
1. <a href="https://github.com/iriusrisk/OpenThreatModel">OpenThreatModel on GitHub</a><br />
2. <a href="https://owasp.org/www-community/Threat_Modeling">Threat Modeling on OWASP</a>
</div>

Threat Modeling is **crucial**
- *Work with experienced security personel*
- Who uses the software? How?
- What assets are involved? How are they protected?
- Identify mitigations and implement them

Your threat model is a living document

Consider publishing it

<aside class="notes">
- There are lots of frameworks and resources out there.<br />
- Memory corruption is a significant threat against "unsafe" code!<br />
- "trust" is not a mitigation!!<br />
- What's the worst thing that could happen?
</aside>


## Implementation Phase

While constructing, be diligent and keep learning.

1. Hopefully you picked a modern language
2. Create and adhere to coding guidelines / standards
3. Conduct code reviews with qualified colleages
4. Pay close attention to compiler warnings
5. Use any and all static analysis tools


## Testing

Write lots of tests
- Unit tests, Integration tests
- **Leverage fuzz testing!**

**USE SANITIZERS**: Address, Thread, UB
- Especially if you're using C or C++

Test your code changes yourself
- Observe your software's behavior first hand
- Who better to know if it's working correctly?

<aside class="notes">
Use saniitizers, but understand that their weakness is that they can only help if tests exercise the code.<br />
<br />
Believe it or not, there are developers out there that think testing is QA's job.
</aside>


## Verification

Formal verification is a desirable property.
 - Coq, Frama-C, CBMC, Kani (for Rust), etc

But it's not a panacea either
- Verifiers are software too


## Post-Deployment

1. Periodically re-assessing security
  - The environment changes, remember qmail?
2. Invite review - open source / bug bounties / etc
  - Marcel wrote about this in his paper, and I agree.
  - This kind of adversarial relationship is virtuous.

Security is a process.

---

<!-- .slide: class="ctitle" -->
# Conclusions
<div class="ctitle-line"></div>

## What I hope you learned


## General Takeways I

Transparency -- we need more
- How is your team investing in security?
- What is your software made of? (SBOM)
- Who audited what?
  - Tracked sometimes, but indirectly (ie. CVE credits)
- What had little or no review?
- What tests run in CI?


## General Takeaways II

Required security classes
- &#x1f4a1; Computer security 101
  - Core concepts
  - History of attacks and defenses
  - Modern best practices

Modern tools incorporate learnings from previous failures
- Feed failures back into security testing pipeline

<aside class="notes">
This would be a good one for engineers to need to take.<br />
</aside>


## Takeaways for Management

<div class="footnote">
1. <a href="https://www.linkedin.com/pulse/top-reasons-why-businesses-should-invest-software-quality-8etde/">Top reasons why businesses should invest in software quality</a>
</div>

Management must set direction appropriately

1. Invest in improving software quality
2. Security bugs are bugs
  - Less bugs means less security bugs

Evidence shows that better quality leads to better efficiency AND cost savings


## Takeaways for Developers

1. More configurable features flags
  - Allow users to toggle features
2. Choose modern languages and tools/toolchains!
3. Learn more about security issues
4. Test, test, fuzz test, use sanitizers.
5. Talk to decision makers about prioritizing quality

<aside class="notes">
Your features may not fit your users risk profile<br />
For example, what features in Chrome are on by default and cannot be disabled??<br />
<br />
Learn, test, and use modern stuff
</aside>


## Takeaways for Security Practitioners

Not enough people?
  - Teach your skills! Take an apprentice!

Let's get scientific!
- Increase rigor, especially in security testing.
- Document them using Hypothesis / Experiment Design / Notes / Results format
- Consider your projects as collections of experiments


## All the safety is not enough

Bugs will still happen

- Command injection, SQL injection, XSS, all the injections
- Logic errors, crypto fails
- Authentication missing or poorly implemented
- ...and so on

**Memory safety issues are reportedly 70% of the problems that Microsoft and Google encounter and fix.**


## Conclusion

Developing secure software is hard work.

Development orgs must take ownership and make wise decisisons.

Modern tools and techniques can help to reduce the burden.

Please take these concepts back to your development orgs and push for improvements.
- Remember: Security is a process and a team sport.

Go read Marcel's paper!!

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

