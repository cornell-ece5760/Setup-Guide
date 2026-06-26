# Introduction

Pre-requisite knowledge, software, setup guides, and TA / past student recommendations to help you thrive in ECE 5760.

---

# Course Policy Reference

> **Note:** Some of these policies are borrowed from Bruce Land and are largely identical to those on the previous course webpage.

---

# Prerequisites

ECE 5725 is strongly recommended. You will need working knowledge of:

- **Verilog / SystemVerilog** — hardware description and sequential logic design
- **C / C++** — software running on the ARM processor side
- **Linux shell commands** — navigating and scripting in a Linux environment
- **Mathematics** — ODEs, PDEs, numerical methods, parallel computation
- **Python** *(optional but a plus)*

When in doubt, talk to the instructor.

---

# Required Software

## Git / GitHub

> "Git is an extremely popular tool for software version control. Its primary purpose is to help engineers track their work, ensuring that they make incremental changes to files that they can later revert if necessary and also to help facilitate combining new code with older versions. When combined with a remote repository, GitHub, it also ensures that an online backup of the work is present."
>
> — Adapted from [Cornell CS 3410, "Git," Fall 2025](https://www.cs.cornell.edu/courses/cs3410/2025fa/rsrc/git.html)

A significant portion of ECE 5760 work lives on GitHub. Private repos will be created for each group — keep them up to date so staff can:
- Track your progress
- Respond to [Issues](https://docs.github.com/en/issues/tracking-your-work-with-issues/learning-about-issues/quickstart) you open in your repo (link an issue to a private EdStem post for TA assistance)

If you need to brush up on Git/GitHub fundamentals, see our quick overview [here](github.md).

---

## Vivado

*(Setup guide coming soon)*

## Vitis

*(Setup guide coming soon)*

---

## Other Software (Optional)

Not required to complete the labs, but potentially useful:

| Tool | Resource |
|---|---|
| **UVM (Verilator)** | [UVM Guide by Chipverify](https://chipverify.com/uvm/uvm-installation) |
| **Cocotb** | [Cocotb Documentation](https://docs.cocotb.org/en/stable/#) |

---

# Reading

Readings cover the theory for each lab and specific implementation techniques. Materials include research papers, Intel/Altera vendor manuals, and instructor-generated web pages.

---

# Purpose

Design of system-on-chip applications for hardware acceleration using FPGAs. Students work in groups of 2–3 to design, debug, and build several systems demonstrating parallel FPGA hardware linked to an ARM processor running Linux. Lectures introduce examples, describe modules to be designed, and cover design tools used in lab.

> This is a **design course**. You will need to show creativity, flexibility, and motivation.

Specifically, you must be able to:
- Search the web to find your own answers to technical questions
- Read and understand manufacturer data sheets for a variety of devices
- Draw on material from many courses you have taken
- Derive solutions from general, incomplete specifications — lab assignments are open-ended

Clever, efficient solutions are rewarded. Designs (C code, Verilog circuitry, and peripheral interfacing) must be worked out before arriving to lab.

---

# Grading

The course has two halves, weighted equally:

| Component | Weight |
|---|---|
| Laboratory assignments (Labs 1–3) | 50% |
| Final project | 50% |

## Laboratory Assignments (50%)

Each lab is broken down as follows:

| Component | Weight per Lab |
|---|---|
| Preparedness & participation | 10% |
| Weekly progress checkoffs | 20% |
| Final lab demonstration | 30% |
| Lab report | 40% |

**Preparedness & participation** — determined by TA conversations in lab, lecture attendance, and occasional in-lecture quizzes. Easy points: just show up.

**Weekly progress checkoffs:**
- Must come to lab prepared — no out-of-class prep means missed deadlines
- On-time checkoff → 95% (A-equivalent); early → >95%; missing → 0
- If you finish a checkpoint before end of lab, stay and work on the next one
- Late checkoffs receive a **zero**

**Final lab demonstration** scoring:

| Technical specs met | Score | Notes |
|---|---|---|
| Below Week 1 checkoff | 0% | |
| Equal to Week 1 checkoff | 50% | |
| Up to Week 2 checkoff | 50–75% | Proportional to specs met, weighted by difficulty |
| Up to Week 3 checkoff | 75–96% | Proportional to specs met, weighted by difficulty |
| Exceeds Week 3 checkoff | 96–100% | A+ equivalent |

- Demos are done in lab before the end of each exercise — no late final demos
- A late demo receives a **zero**; if you run out of time, demonstrate what works

**Lab report:**
- Due before the start of your next lab period
- One report per team; no written collaboration between groups
- Submitted electronically to your TA via Canvas
- A late report receives a **zero**

---

## Final Project (50%)

| Component | Weight |
|---|---|
| Preparedness & participation | 10% |
| Weekly progress milestones | 20% |
| Final demonstration | 30% |
| Final report | 40% |

- You are responsible for establishing your own weekly milestones
- Report progress weekly (written or verbal)
- Final demo is also evaluated on sophistication relative to other projects
- Create a webpage for your final project

> **Note:** Plans change and things are sometimes harder than expected. As long as you are communicating and working at a reasonable rate, grade will not be adversely affected by changes of plan.

---

## Final Grade Breakdown by Component

| Component | Lab 1 | Lab 2 | Lab 3 | Final Project |
|---|---|---|---|---|
| Preparedness / Participation | 1.7% | 1.7% | 1.7% | 5% |
| Checkout 1 | 1.1% | 1.1% | 1.1% | — |
| Checkout 2 | 1.1% | 1.1% | 1.1% | — |
| Checkout 3 | 1.1% | 1.1% | 1.1% | — |
| Weekly Progress | — | — | — | 10% |
| Final Demo | 5% | 5% | 5% | 15% |
| Lab / Final Report | 6.7% | 6.7% | 6.7% | 20% |

> Missing one checkpoint is not catastrophic — do the math and keep perspective.

---

# Laboratory Policies

- **Do not** enter the lab during ECE 2300 class time — doing so results in a 0 for that week's checkoff and loss of lab access
- Attend your assigned lab period every week and finish the assignment in the allotted time
- You may start assignments early; notify your instructor in advance for planned absences

**During checkoff lab sections:**
- TAs' first priority is checking people off
- TAs help only if no one is waiting for checkoff
- Students in the current section trying to finish on time are helped first
- Students from other sections are helped last

Lab work is in **groups of 2–3**. All members must become proficient in all aspects of the lab. Members may be graded differentially if one person is clearly doing the bulk of the work.

---

# Academic Integrity

Each student must abide by the [Cornell University Code of Academic Integrity](https://cuinfo.cornell.edu/aic.cfm). All submitted work will be the student's own. Submissions may be checked via Turnitin.com.

## Collaboration — What's Allowed

| Allowed | Not Allowed |
|---|---|
| Sharing all homework and code **within** your group | Sharing any material **between** groups |
| Talking in lab about code with another group | Emailing code to another group or typing on their keyboard |
| Showing another group your circuit | Wiring for another group or lending them your circuit |
| Discussing lab report contents with another group | Copying even one sentence from any web or print source without citation |
| Using code from previous final projects or web sources **with** attribution | Using code from previous final projects or web sources **without** attribution |

> Unprotected GitHub or other public code repositories will be considered a violation of Cornell's academic integrity policy.

---

# AI Policies

### For Lab Reports

AI-generated content must be cited and quoted in exactly the same way as human-generated content. Failure to do so **is plagiarism**.

### For Code

You may use AI-generated code at your own risk, subject to:
- All AI-generated code must be clearly labeled (see format below) — unlabeled AI code **is plagiarism**
- Course staff will **not** help you debug AI-generated code
- Along with your lab report, submit a **prompt log** (see below)

**Required label format:**
```
################## BEGIN AI-GENERATED CODE ##################
void foo() {
  printf("Hello, humans.") ;
}
################### END AI-GENERATED CODE ###################
```

**Generating a prompt log** — run this prompt in Copilot (or equivalent):
> *"Generate a prompt log of this conversation. For each prompt, include the time/date, the number of edits suggested, and the number of code insertions, deletions, and modifications accepted."*

---

# Laboratory Reports

One written report per group, submitted electronically via Canvas. Write to a level of detail such that in two years, you could recreate the project using only your report.

## Suggested Report Structure

1. **Introduction** — short explanation of what was done and the roles of the ARM and FPGA sides
2. **RTL Description** — RTL-level description of your project and any relevant state machines
3. **Design and Testing Methods** — your approach for both software and hardware; include tests whose outcomes are convincing that requirements were met
4. **Results** — screenshots, videos, frequency analysis, or whatever documents the functioning system
5. **Documentation** — drawings, program listings, and explanatory comments
6. **Answers** — responses to specific questions from the lab writeup
7. **Comments** *(optional)* — suggestions for improvement, excuses, complaints

Example well-done reports from ECE 4760 are available on the course webpage. Aim for that level of depth. Note that those examples predate the AI citation requirement.

---

# Access to Computers

You and your partner(s) have access to a PC, FPGA, etc. in Phillips 238 during your assigned lab period. Setups not needed by current-section students may be used by others.

> **Back up your work.** Machines and file systems die. There is no excuse for lost work, even due to a compiler or system error.

---

# Academic Concerns

If you are experiencing undue personal or academic stress, seek support early. Available resources include:

- Your college's Academic Advising or Student Services Office
- **Cornell Learning Strategies Center** — 255-6310 | [lsc.sas.cornell.edu](http://lsc.sas.cornell.edu)
- **Gannett Health Services** — 255-5155 | [gannett.cornell.edu](http://www.gannett.cornell.edu)
- **Let's Talk Drop-In Consultation** — [gannett.cornell.edu/Let'sTalk](http://www.gannett.cornell.edu/Let'sTalk)
- **EARS Peer Support** — 255-EARS
- **Student Disability Services (SDS)** — 420 CCC Building, 254-4545 (confidential)

---

*Authors: Hunter Adams, Dennis Bui, Anthony Song*
*Last Updated: Jun 24, 2026*
