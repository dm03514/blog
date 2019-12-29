# How I Interview: Technical Level Setting



# Problem

Technical interviews are often ambiguous and poorly structured without having explicit goals.  The following outlines a methodology that I've used successfully over 30 interviews and 3 hires.  Even though this isn't a huge sample set I'm really happy with the signals that this methodology gives me and would like to share it. The methodology is called Invariants and Gradients, and this specific stage is focused on Level Setting, (establishing that the candidate is at a certain technical level or proficiency).  This is accomplished through asking open ended questions which encourage the candidates level, and current abilities, to **emerge**.


# What's the point??

What's even the point of a technical interview? 

Technical interviews often act as a check and balance system to verify that candidates are making factual claims about their experience.  

Consider a candidate that applies with nothing known about them, vs a candidate that is super well known within the industry:

<p align="center">
  <img src="static/nothing_vs_everything.png">
</p>

Obviously, most candidates fall somewhere in between not knowing anything at all about the candidate and having perfect information of their technical abilities.  Based on the information that they present some sort of understanding of their technical experience can be inferred. We don't fully believe the candidate, because if we did we'd evaluate them technically based on the experience that they present.

The technical interviews purpose is to:

- Establish that the candidate has the requisite experience to perform the functions of the job

I consider there to be two major parts within this:

- Materializing an understanding of the candidates holistic technical abilities I call this Level Setting and its purpose is to ensure that the candidates level is understood, ie entry, junior, mid, engineer II, senior, etc.A
- Demonstrate specific understanding of technical proficiencies.  This establishes that the candidate has specific technical abilities required of the position. If the code base they are working in is a distributed system and their is significant risk from incorrectness the candidate *needs* to demonstrate proficiency in distributed system.  


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

It's important that these are objective and can either be hit or missed.  Consider some technical interviews that ask questions about specific technologies like:

- What are some common HTTP verbs and how are they typically used in REST API's?
- How would you request that a server return an API call results in JSON format?
- Which request header is used to transmit credentials to a server?

What would a candidate answering "I don't know" to any of these questions indicate about the candidate? What if they were only able to list 2 of the request verbs? 5? Because of how expensive interviewing is, there's a huge opportunity cost to asking questions like this during technical interviews.  Invariants are used to prune candidates in an objective fair and high fidelity way.


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
- Explain the steps of a request and response from curl to a web service like google.

Each of the gradients may have one or more specific invariants.  An invariant for **How do you ensure that a solution functions correctly?** may be:

- Must mention automated testing

Because the question are so open ended the candidate usually has to choose a level of abstrction that they are most familiar with, which provides a strong signal in itself.

Gradient scoped invariants are where specific role requirements can be expressed.  Consider the example of the HTTP Request/Response.  If this question is asked to a backednd we candidate and they fail to mention load balancing tiers.  The goal of this methodology is to make these requirements explicit and increase objectivity of evaluation.  

To illustrate how gradients may be evaluated, consider the question:

**How do you ensure that a solution functions correctly?**

Common answers may be:

- Unit Tests
- TDD
- Service Tests
- CI/CD
- Reliance on QA
- Manual Verification
- Monitoring

Strong Level Setting indicators may be:

- Not Mentioning Tests - Entry
- Mentioning: Run it and Watch with Logs - Entry
- Tests & No Monitoring - Mid

# Conclusion

I have found technical level setting to be a crucial step in materializing an understanding of candidates technical abilities. Technical Level setting is not a replacement for demonstrating specific technical requisites but can be a powerful fun interview step that provides low false positives and negatives for qualifying candidates for specific roles.  Technical Leveleing is based on ensuring candidates comply with invariants ccombined with questions that allow candidates abilities to emerge.  A large number of the interviews that I gave ~5 / 30 (16%) I received direct feedback from the candidate describing these as fun!!! This stage is often a fun free feeling discussion.  Happy Interviewing!
