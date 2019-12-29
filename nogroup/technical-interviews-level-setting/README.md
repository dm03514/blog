# How I Interview: Technical Level Setting



# Problem

Technical interviews are often ambiguous and poorly structured without having explicit goals.  The following outlines a methodology that I've used successfully over 30 interviews and 3 hires.  Even though this isn't a huge sample set I'm really happy with the signals that this methodology gives me and would like to share it. The methodology is called Invarients and Gradients, and this speciic stage is focused on Level Setting, (establishing that the candidate is at a certain technical level or proficiency).  This is accomplished through asking open ended questions which encourage the candidates level, and current abilities, to **emerge**.


# What's the point??

What's even the point of a technical interview? 

Technical interviews often act as a check and balance system to verify that candidates are making factual claims about their experience.  

Consider a candidate that applies with nothing known about them, vs a candidate that is super well known within the industry

<p align="center">
  <img src="static/nothing_vs_everything.png">
</p>

Obviously, most candidates fall somewhere in between not knowing anything at all about the candidate and having perfect information of their technical abilities.  Based on the information that they present some sort of understanding of their technical experience can be inferred. We don't fully believe the candidate, because if we did we'd evaluate them technically based on the experience that they present.

The technical interviews purpose is to:

- Establish that the candidate has the requisite experience to perform the functions of the job

I consider there to be two major parts within this:

- Materializing an understanding of the candidates holistic technical abilities I ccall this Level Setting and its purpose is to ensure that the candidates level is understood, ie entry, junior, mid, engineer II, senior, etc.A
- Demonstrate specific understanding of technical proficienceies.  This establishes that the candidate has specific technical abilities required of the position. If the code base they are working in is a distributed system and their is significant risk from incorrectness the candidate *needs* to demonstrate proficiency in distributed system.  


# Methodology Goal 

The goal is to create an exercise that provides high signal on a candidates level and minimizes the noise. This is because of the extreme time constraint placed on the interview process.  Candidates are most likely interviewing at many places.  Then on the hiring side interviews are extremely expensive and time consuming.  With the minimal amount of time we want to develop an accurate, high fidelity signal of how a candidates level by exploring how they approach technical problems and create solutions.

# Implementation

 The solution creates an open ended scenario that encourages a candidates technical ability to **emerge**, meaning it allows the candidates competencies to emerge from the assignment.  It's necessarily something that the candidate can't study for.
 
 This uses a technical task as a foundation to allow us to determine with good accuracy where the candidate is right now.  This is not for trying to guess what the candidate may be capable of in the future (that can be estimated from their past trajectory).  This is also not for getting very specific technical information from them (which need to be demonstrated directly, either by asking or by demonstration).

 All are open ended because all encourage emergent based on:
- The candidate will mention what they have the most experience with (80%) this indicates the way the candidate thinks and how they would actually approach the problem, because they aren't something that can be prepared for.
- The candidate will mention what they think is the most important (20%)
- The candidate mentions what they think we want to hear (not observed)

## Invariants

<p align="center">
  <img src="static/rules.png" width="300px">
</p>

The foundation of the approach are Invariants.  These are things that the candidate *must* display in order to qualify.  These are a hard line in the sand.

Some of the general Invariants that I have used are:
- Asks clarifying questions
- Verifies solution runs / works (for a coding exercise)


## Gradients 

<p align="center">
  <img src="static/foggy_stairs.jpg" width="300px">
</p>

Gradients define the signals that are important for the target role. The goal of gradients is to try and formalize the signals.    For example Software Engineering, these are open ended and aim to have the candidates ability naturally emerge and place itself, the whole idea is for these to be things that people really can't study for..

Gradients are questions that can't be studied for which encourage immediate reflexive answers.  There are no wrong answers here because the purpose is to place a candidate.  I've found these discussions to be really fun and the candidate to be really engaged.

Examples are:

- How do you ensure that a solution functions correctly?
- How do you tell if a deployment is successful?
- Suppose that you’re creating an HTTP service and recently made a successfully deploy but some time later customers start to report a degradation of service, how do you go about figuring out the source of the issue? 


