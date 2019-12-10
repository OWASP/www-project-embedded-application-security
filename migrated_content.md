---

layout: col-sidebar
title: OWASP Embedded Application Security
tags: example-tag
level: 0
type: documentation

---
# Main

<div style="width:100%;height:100px;border:0,margin:0;overflow: hidden;">

![Incubator_big.jpg](Incubator_big.jpg "Incubator_big.jpg")

</div>

<table>
<tbody>
<tr class="odd">
<p>Every year the prevalent use of embedded software within enterprise and consumer devices continues to rise exponentially. With widespread publicity of the Internet of Things (IoT), more and more devices are becoming network connected evidencing how essential it is to create secure coding guidelines for embedded software. Embedded Application Security is often not a high priority for embedded developers when they are producing devices such as routers, managed switches, medical devices, Industrial Control Systems (ICS), VoIP phones, IoT devices, and ATM Kiosks due to other challenges outside of development. Other challenges developers face may include, but are not limited to, the Original Design Manufacturer (ODM) supply chain, limited memory, a small stack, and the challenge of pushing firmware updates securely to an endpoint. The goals of this project are to create a list of best practices, provide practical guidance to embedded developers, and to draw on the existing OWASP resources that can bring application security expertise to the embedded world. It is important to note, each of the items and guidance points listed below are longstanding within software security. This document purely tailors issues that OWASP has previously provided guidance upon (e.g. OWASP Top 10, Mobile Top 10, etc.) to the embedded community. <em>Given the prevalence of Linux kernels utilized within embedded devices, all code examples are geared towards a POSIX environment but the principles are designed to be platform agnostic.</em></p>
<p>For the most up to date best practices document, please visit <a href="https://scriptingxss.gitbooks.io/embedded-appsec-best-practices//"><a href="https://scriptingxss.gitbooks.io/embedded-appsec-best-practices/">https://scriptingxss.gitbooks.io/embedded-appsec-best-practices/</a></a></p></td>
<td><h2 id="mailing_list_group_communication">Mailing List / Group Communication</h2>
<p><a href="https://groups.google.com/a/owasp.org/forum/?hl=en#!forum/embedded-appsec">Embedded Sec Mailing List</a> <a href="http://owasp.herokuapp.com/">Please join our OWASP Slack channel; look for the #embeddedappsec</a></p>
<p><a href="https://groups.google.com/a/owasp.org/forum/?hl=en#!forum/embedded-appsec">Embedded Sec Mailing List</a> <a href="http://owasp.herokuapp.com/">Please join our OWASP Slack channel; look for the #embeddedappsec</a></p>
<h2 id="project_leaders">Project Leaders</h2>
<h2 id="project_leaders">Project Leaders</h2>
<p><a href="https://owasp.org/index.php/User:Aaron.guzman">Aaron Guzman</a> <a href="mailto:aaron.guzman@owasp.org">@</a><br />
<p><a href="https://owasp.org/index.php/User:Aaron.guzman">Aaron Guzman</a> <a href="mailto:aaron.guzman@owasp.org">@</a><br />
<a href="https://owasp.org/index.php/User:Alex.Lafrenz">Alex Lafrenz</a> <a href="mailto:alex.lafrenz@owasp.org">@</a></p>
<a href="https://owasp.org/index.php/User:Alex.Lafrenz">Alex Lafrenz</a> <a href="mailto:alex.lafrenz@owasp.org">@</a></p>
<h2 id="related_projects">Related Projects</h2>
<h2 id="related_projects">Related Projects</h2>
<ul>
<ul>
<li><a href="OWASP_Internet_of_Things_Project" title="wikilink">OWASP Internet of Things Project</a></li>
<li><a href="OWASP_Internet_of_Things_Project" title="wikilink">OWASP Internet of Things Project</a></li>
<li><a href="C-Based_Toolchain_Hardening" title="wikilink">C-Based Toolchain Hardening</a></li>
<li><a href="C-Based_Toolchain_Hardening" title="wikilink">C-Based Toolchain Hardening</a></li>
<li><a href="OWASP_Mobile_Security_Project" title="wikilink">OWASP Mobile Security Project</a></li>
<li><a href="OWASP_Mobile_Security_Project" title="wikilink">OWASP Mobile Security Project</a></li>
<li><a href="IoT_Firmware_Analysis" title="wikilink">IoT Firmware Analysis</a></li>
<li><a href="IoT_Firmware_Analysis" title="wikilink">IoT Firmware Analysis</a></li>
</ul></td>
</ul></td>
<h2 id="releases">Releases</h2>
<p><a href="https://scriptingxss.gitbooks.io/top-10-embedded-appsec-best-practices/content/">Living Document (GitBook)</a></p>
<p><a href="https://www.gitbook.com/download/pdf/book/scriptingxss/top-10-embedded-appsec-best-practices">Version 1 (2017)</a></p>
<p>Version 2 scheduled for Fall 2018</p></td>
</tr>
</tbody>
</table>

# Embedded Best Practices

# Embedded Top 10 Best Practices

[Click here to find additional details pertaining to each of the top ten
categories listed
below](https://scriptingxss.gitbooks.io/embedded-application-security-best-practices/content/)

## E1 – Buffer and Stack Overflow Protection

Prevent the use of known dangerous functions and APIs in effort to
protect against memory-corruption vulnerabilities within firmware. (e.g.
Use of unsafe C functions - strcat, strcpy, sprintf, scanf)
Memory-corruption vulnerabilities, such as buffer overflows, can consist
of overflowing the stack (Stack overflow) or overflowing the heap (Heap
overflow). For simplicity purposes, this document does not distinguish
between these two types of vulnerabilities. In the event a buffer
overflow has been detected and exploited by an attacker, the instruction
pointer register is overwritten to execute the arbitrary malicious code
provided by the attacker.

## E2 – Injection Prevention

Ensure all untrusted data and user input is validated, sanitized, and/or
outputs encoded to prevent unintended system execution. There are
various injection attacks within application security such as operating
system (OS) command injection, cross-site scripting (E.g. JavaScript
injection), SQL injection, and others such as XPath injection. However,
the most prevalent of the injection attacks within embedded software
pertain to OS command injection; when an application accepts
untrusted/insecure input and passes it to external applications (either
as the application name itself or arguments) without validation or
proper escaping.

## E3 – Firmware Updates and Cryptographic Signatures

Ensure robust update mechanisms utilize cryptographically signed
firmware images upon download and when applicable, for updating
functions pertaining to third party software. Cryptographic signature
allows for verification that files have not been modified or otherwise
tampered with since the developer created and signed them. The signing
and verification process uses public-key cryptography and it is
difficult to forge a digital signature (e.g. PGP signature) without
first gaining access to the private key. In the event a private key is
compromised, developers of the software must revoke the compromised key
and will need to re-sign all previous firmware releases with the new
key.

## E4 – Securing Sensitive Information

Do not hardcode secrets such as passwords, usernames, tokens, private
keys or similar variants into firmware release images. This also
includes the storage of sensitive data that is written to disk. If
hardware security element (SE) or Trusted Execution Environment (TEE) is
available, it is recommended to utilize such features for storing
sensitive data. Otherwise, use of strong cryptography should be
evaluated to protect the data. If possible, all sensitive data in
clear-text should be ephemeral by nature and reside in a volatile memory
only.

## E5 – Identity Management

User accounts within an embedded device should not be static in nature.
Features that allow separation of user accounts for internal web
management, internal console access, as well as remote web management
and remote console access should be available to prevent automated
malicious attacks.

## E6 – Embedded Framework and C-Based Hardening

Limit BusyBox, embedded frameworks, and toolchains to only those
libraries and functions being used when configuring firmware builds.
Embedded Linux build systems such as Buildroot, Yocto and others
typically perform this task. Removal of known insecure libraries and
protocols such as Telnet not only minimize attack entry points in
firmware builds, but also provide a secure-by-design approach to
building software in efforts to thwart potential security threats.

## E7 – Usage of Debug Code and Interfaces

It is important to ensure all unnecessary pre-production build code, as
well as dead and unused code, has been removed prior to firmware release
to all market segments. This includes but is not limited to potential
backdoor code and root privilege accounts that may have been left by
parties such as Original Design Manufacturers (ODM) and Third-Party
contractors. Typically this falls in scope for Original Equipment
Manufacturers (OEM) to perform via reverse engineering of binaries. This
should also require ODMs to sign Master Service Agreements (MSA)
insuring that either no backdoor code is included and that all code has
been reviewed for software security vulnerabilities holding all
Third-Party developers accountable for devices that are mass deployed
into the market.

## E8 – Transport Layer Security

Ensure all methods of communication are utilizing industry standard
encryption configurations for TLS. The use of TLS ensures that all data
remains confidential and untampered with while in transit. Utilize free
certificate authority services such as Let’s Encrypt if the embedded
device utilizes domain names.

## E9 – Data collection Usage and Storage - Privacy

It is critical to limit the collection, storage, and sharing of both
personally identifiable information (PII) as well as sensitive personal
information (SPI). Leaked information such as Social Security Numbers
can lead to customers being compromised which could have legal
repercussions for manufacturers. If information of this nature must be
gathered, it is important to follow the concepts of Privacy-by-Design.

## E10 – Third Party Code and Components

Following setup of the toolchain, it is important to ensure that the
kernel, software packages, and third party libraries are updated to
protect against publicly known vulnerabilities. Software such as
Rompager or embedded build tools such as Buildroot should be checked
against vulnerability databases as well as their ChangeLogs to determine
when and if an update is needed. It is important to note this process
should be tested by developers and/or QA teams prior to release builds
as updates to embedded systems can cause issues with the operations of
those systems. Embedded projects should maintain a “Bill of Materials”
of the third party and open source software included in its firmware
images. This Bill of Materials should be checked to confirm that none of
the third party software included has any unpatched vulnerabilities. Up
to date vulnerability information may be found through the National
Vulnerability Database or Open Hub.

Several solutions exist for cataloging and auditing third party
software: Retirejs for Javascript projects (free) Black Duck (paid)
Package Managers (free) Buildroot (free)

# Embedded Device Firmware Analysis Tools

Over the years, embedded security hardware and software tools have been
introduced. Some free, some commercially based. If the lists below are
missing tools from your arsenal, please feel free to add them.

### Hardware

  - JTagulator [1](http://www.grandideastudio.com/jtagulator/)
  - UART to USB
      - Shikra [2](http://int3.cc/products/the-shikra)
  - TTL RS323
  - C232HM Cable
  - JTAG Adapters
      - JLINK
      - Jtagulator
      - Flyswatter2
  - BusPirate
  - BusBlaster
  - CPLDs (in lieu of FPGAs)
  - Oscilloscopes
  - Multimeter (Ammeter, Voltmeter, etc)
  - Logic Analyzers [3](https://www.saleae.com/logic16)
  - OpenOCD
  - GreatFET [4](https://greatscottgadgets.com/greatfet/)
  - Solder station
  - Hot air rework gun
  - Clips
  - Leads
  - Headers
  - hooks

### Software

  - Angr - [5](https://github.com/angr/angr)
  - Firmadyne [6](https://github.com/firmadyne/firmadyne)
  - Firmwalker [7](https://github.com/craigz28/firmwalker)
  - [Firmware Analysis
    Toolkit](https://github.com/attify/firmware-analysis-toolkit)
  - Binary Analysis
    [8](http://www.binaryanalysis.org/en/content/show/download)
  - Flawfinder [9](https://sourceforge.net/projects/flawfinder/)
  - IDA Pro (supports ARM / MIPS)
  - Radare2 [10](https://github.com/radare/radare2)
  - Buildroot
  - GDB
  - Binwalk [11](http://binwalk.org/)
  - Firmware-mod-toolkit
    [12](https://code.google.com/archive/p/firmware-mod-kit/)
  - Capstone framework [13](http://www.capstone-engine.org/)
  - [Firmware Analysis and Comparison
    Tool](https://github.com/fkie-cad/FACT_core)
  - [Firmware Analysis
    Toolkit](https://github.com/attify/firmware-analysis-toolkit)

# Roadmap

## 2018 Roadmap

Introductory Embedded Section

  - \[x\] Expand on what embedded firmware is (8,16,32 bit, minimal
    hardware resources, list embedded use cases and industries)
  - \[x\] Describe types of architectures (MIPS, ARM, PowerPC, x86 etc.)
  - \[x\] Describe types of firmware and operating systems
  - \[ \] Layout of firmware for embedded linux, RTOS, and Embedded
    Window

Expand on embedded best practices

  - \[ \] Secure boot recommendations
      - \[x\] U-boot
  - \[x\] Create examples of software bill of materials (BOM)
  - \[x\] Additional example programming language command injection
    system calls or APIs
  - \[ \] Break out subsections for each of the platforms with
    contextual guidance and configurations
  - \[ \] Expand on hardening for:
      - \[ \] Embedded Linux
      - \[ \] RTOS (QNX/MQX)
  - \[ \] Best practices/considerations for PKI in embedded systems

Create example embedded application security requirements for new
products

  - \[ \] Integrate with ASVS or create an EASVS (Embedded Application
    Security Verification Standard)
  - \[ \] Integrate with the IoT project

Join the mailing list, slack channel (\#embeddedappsec) and contact the
Project leaders if you feel you can contribute.

# Contributing

You do not have to be a security expert in order to contribute\!

Some of the ways you can help:

  - Technical editing
  - Review
  - Diagrams
  - Graphic design
  - Code snippets in your favorite language
  - Translate guidance material

Feel free to sign up for a task out of our roadmap below or add your own
idea to the roadmap. To get started, create a GitBook account or sign in
with your Github credentials to add comments and make edits. All changes
are tracked and synced
to https://github.com/scriptingxss/embeddedappsec. Alternatively, clone
the Github repo, use your favorite markdown editor, apply/make your
edits, and submit a pull request. Feel free to contact the project
leaders for ways to get involved. __NOTOC__
<headertabs></headertabs>

[Category:OWASP_Project](Category:OWASP_Project "wikilink")
