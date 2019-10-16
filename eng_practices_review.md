# [Google’s Code Review Guidelines](https://google.github.io/eng-practices/)

- What Do Code Reviewers Look For?

  - **Design**: Is the code well-designed and appropriate for your system?

  - **Functionality**: Does the code behave as the author likely intended? Is the way the code behaves good for its users?

    - Mostly, just by reading the code
    - Sometimes (e.g. UI change), validate either by trying it yourself or asking for a demo
    - Parallel programming, careful for the problems of race conditions or deadlocks

  - **Complexity**: Could the code be made simpler? Would another developer be able to easily understand and use this code when they come across it in the future?

    - "Too complex" usually means

      - Can’t be understood quickly by code readers.
      - Developers are likely to introduce bugs when they try to call or modify this code.

    - Over-engineering

      Do NOT

      - Make the code more generic than it needs to be
      - Add functionality that isn’t presently needed by the system

  - **Tests**: Does the code have correct and well-designed automated tests?

  - **Naming**: Did the developer choose clear names for variables, classes, methods, etc.?

  - **Comments**: Are the comments clear and useful?

    Usually comments are useful when they _explain why_ some code exists, and should not be explaining _what_ some code is doing.

  - **Style**: Does the code follow our [style guides](http://google.github.io/styleguide/)?

  - **Documentation**: Did the developer also update relevant documentation?

## The Code Reviewer’s Guide

### The Standard of Code Review

**In general, reviewers should favor approving a CL once it is in a state where it definitely improves the overall code health of the system being worked on, even if the CL isn’t perfect.**

- Prefix "Nit:" - A point of polish that authors could choose to ignore

- Resolving Conflicts

  Don’t let a CL sit around because the author and the reviewer can’t come to an agreement.

  - Face-to-face Meeting
  - Escalation

### What to Look For In a Code Review

- Every Line

  At Google, we hire great software engineers, and you are one of them. If you can’t understand the code, it’s very likely that other developers won’t either. So you’re also helping future developers understand this code, when you ask the developer to clarify it.

- Context

  Don’t accept CLs that degrade the code health of the system.

- Good Things

  Code reviews often just focus on mistakes, but they should offer encouragement and appreciation for good practices, as well.

- Summary

  - The code is well-designed.
  - The functionality is good for the users of the code.
  - Any UI changes are sensible and look good.
  - Any parallel programming is done safely.
  - The code isn’t more complex than it needs to be.
  - The developer isn’t implementing things they might need in the future but don’t know they need now.
  - Code has appropriate unit tests.
  - Tests are well-designed.
  - The developer used clear names for everything.
  - Comments are clear and useful, and mostly explain why instead of what.
  - Code is appropriately documented (generally in g3doc).
  - The code conforms to our style guides.

  Make sure to review **every line** of code you’ve been asked to review, look at the **context**, make sure you’re **improving code health**, and compliment developers on **good things** that they do.

### Navigating a CL in Review

- Step 1: Take a broad view of the change

  Courtesy is important because we want to show that we respect each other as developers even when we disagree.

  - For example, you might say "Looks like you put some good work into this, thanks! However, we’re actually going in the direction of removing the FooWidget system that you’re modifying here, and so we don’t want to make any new modifications to it right now. How about instead you refactor our new BarWidget class?"

- Step 2: Examine the main parts of the CL

- Step 3: Look through the rest of the CL in an appropriate sequence

### Speed of Code Reviews

- Why Should Code Reviews Be Fast?

  When code reviews are slow, several things happen:

  - The velocity of the team as a whole is decreased.
  - Developers start to protest the code review process.
  - Code health can be impacted.

- How Fast Should Code Reviews Be?

  **One business day is the maximum time it should take to respond** to a code review request (i.e. first thing the next morning).

- Speed vs. Interruption

  If you are in the middle of a focused task, such as writing code, don’t interrupt yourself to do a code review.

- Fast Responses

  It’s even more important for the individual responses to come quickly than it is for the whole process to happen rapidly.

  It is important that reviewers spend enough time on review that they are certain their "LGTM" means "this code meets our standards."

- Cross-Time-Zone Reviews

- LGTM With Comments

- Large CLs

  One of your goals as a reviewer should be to always unblock the developer or enable them to take some sort of further action quickly, without sacrificing code health to do so.

- Code Review Improvements Over Time

  **Don’t compromise on the code review standards or quality for an imagined improvement in velocity**—it’s not actually going to make anything happen more quickly, in the long run.

- Emergencies

  - What Is An Emergency?

    An emergency CL would be a **small** change that, e.g.

    - Allows a major launch to continue instead of rolling back.
    - Fixes a bug significantly affecting users in production.
    - Handles a pressing legal issue.
    - Closes a major security hole.

  - What Is Not An Emergency?

    For example:

    - Wanting to launch this week rather than next week (unless there is some actual hard deadline for launch such as a partner agreement).
    - The developer has worked on a feature for a very long time and they really want to get the CL in.
    - The reviewers are all in another timezone where it is currently nighttime or they are away on an off-site.
    - It is the end of the day on a Friday and it would just be great to get this CL in before the developer leaves for the weekend.
    - A manager says that this review has to be complete and the CL checked in today because of a soft (not hard) deadline.
    - Rolling back a CL that is causing test failures or build breakages.

  - What Is a Hard Deadline?

    A hard deadline is one where **something disastrous would happen** if you miss it.

    For example:

    - Submitting your CL by a certain date is necessary for a contractual obligation.
    - Your product will completely fail in the marketplace if not released by a certain date.
    - Some hardware manufacturers only ship new hardware once a year. If you miss the deadline to submit code to them, that could be disastrous, depending on what type of code you’re trying to ship.

    Most deadlines are soft deadlines, not hard deadlines. They represent a desire for a feature to be done by a certain time. They are important, but you shouldn’t be sacrificing code health to make them.

### How to Write Code Review Comments

- Courtesy

  - Be kind.

  - Make comments about the _code_ and never making comments about the _developer_.

    For Example:

    - Bad: "Why did **you** use threads here when there’s obviously no benefit to be gained from concurrency?"

    - Good: "The concurrency model here is adding complexity to the system without any actual performance benefit that I can see. Because there’s no performance benefit, it’s best for this code to be single-threaded instead of using multiple threads."

- Explain Why

  - Explain your reasoning.

- Giving Guidance

  - Balance giving explicit directions with just pointing out problems and letting the developer decide.

  - **In general it is the developer’s responsibility to fix a CL, not the reviewer’s.**

- Accepting Explanations

  - Encourage developers to simplify code or add code comments instead of just explaining the complexity to you.

  - **Rewrite the code more clearly.**

  - **Explanations written only in the code review tool are not helpful to future code readers.**

### Handling Pushback in Code Reviews

- Who is right?

  When a developer disagrees with your suggestion,

  - First take a moment to consider if developers are correct.

  - **Improving code health tends to happen in small steps.**

  - Always stay polite.

  - Let the developer know that you _hear_ what they’re saying, you just don’t _agree_.

- Upsetting Developers

  - Reviewers sometimes believe that the developer will be upset if the reviewer insists on an improvement.

  - Sometimes developers do become upset, but it is usually brief and they become very thankful later that you helped them improve the quality of their code.

  - Usually, if you are polite in your comments, developers actually don’t become upset at all, and the worry is just in the reviewer’s mind.

  - Upsets are usually more about the way comments are written than about the reviewer’s insistence on code quality.

- Cleaning It Up Later

  - In fact, usually unless the developer does the clean up _immediately_ after the present CL, it never happens.

  - Thus, it is usually best to insist that the developer clean up their CL _now_, before the code is in the codebase and "done."

  - Letting people "clean things up later" is a common way for codebases to degenerate.

  - If the CL exposes surrounding problems and they can’t be addressed right now, the developer should file a bug for the cleanup and assign it to themselves so that it doesn’t get lost.

- General Complaints About Strictness

  - Improving the speed of your code reviews usually causes these complaints to fade away.

  - Sometimes it can take months for these complaints to fade away, but eventually developers tend to see the value of strict code reviews as they see what great code they help generate.

  - Sometimes the loudest protesters even become your strongest supporters once something happens that causes them to really see the value you’re adding by being strict.

- Resolving Conflicts

  See The Standard of Code Review for guidelines and principles that can help resolve the conflict.

## The Change Author’s Guide

### Writing Good CL Descriptions

- First Line

  - Short summary of what is being done.
  - Complete sentence, written as though it was an order.
  - Follow by empty line.

  For example:

  - Good: "**Delete** the FizzBuzz RPC and **replace** it with the new system."
  - Bad: "**Deleting** the FizzBuzz RPC and **replacing** it with the new system."

- Body is Informative

- Bad CL Descriptions

  For example:

  - "Fix bug."
  - "Fix build."
  - "Add patch."
  - "Moving code from A to B."
  - "Phase 1."
  - "Add convenience functions."
  - "kill weird URLs."

- Good CL Descriptions

  - Functionality change

    Example:

    > rpc: remove size limit on RPC server message freelist.
    >
    > Servers like FizzBuzz have very large messages and would benefit from reuse. Make the freelist larger, and add a goroutine that frees the freelist entries slowly over time, so that idle servers eventually release all freelist entries.

  - Refactoring

    Example:

    > Construct a Task with a TimeKeeper to use its TimeStr and Now methods.
    >
    > Add a Now method to Task, so the borglet() getter method can be removed (which was only used by OOMCandidate to call borglet’s Now method). This replaces the methods on Borglet that delegate to a TimeKeeper.
    >
    > Allowing Tasks to supply Now is a step toward eliminating the dependency on Borglet. Eventually, collaborators that depend on getting Now from the Task should be changed to use a TimeKeeper directly, but this has been an accommodation to refactoring in small steps.
    >
    > Continuing the long-range goal of refactoring the Borglet Hierarchy.

  - Small CL that needs some context

    Example:

    > Create a Python3 build rule for `status.py`.
    >
    > This allows consumers who are already using this as in Python3 to depend on a rule that is next to the original status build rule instead of somewhere in their own tree. It encourages new consumers to use Python3 if they can, instead of Python2, and significantly simplifies some automated build file refactoring tools being worked on currently.

- Review the description before submitting the CL

### Small CLs

- Why Write Small CLs?

  Small, simple CLs are:

  - Reviewed more quickly.
  - Reviewed more thoroughly.
  - Less likely to introduce bugs.
  - Less wasted work if they are rejected.
  - Easier to merge.
  - Easier to design well.
  - Less blocking on reviews.
  - Simpler to roll back.

  **Reviewers have discretion to reject your change outright for the sole reason of it being too large.**

- What is Small?

  In general, the right size for a CL is **one self-contained change**.

- When are Large CLs Okay?

  - You can usually count deletion of an entire file as being just one line of change, because it doesn’t take the reviewer very long to review.
  - Sometimes a large CL has been generated by an automatic refactoring tool that you trust completely, and the reviewer’s job is just to sanity check and say that they really do want the change. These CLs can be larger, although some of the caveats from above (such as merging and testing) still apply.

- Separate Out Refactorings

  - It’s usually best to do refactorings in a separate CL from feature changes or bug fixes.

  - Small cleanups such as fixing a local variable name can be included inside of a feature change or bug fix CL, though.

- Keep related test code in the same CL

- Don’t Break the Build

- Can’t Make it Small Enough

  - Sometimes you will encounter situations where it seems like your CL _has_ to be large. This is very rarely true.

  - Before writing a large CL, consider whether preceding it with a refactoring-only CL could pave the way for a cleaner implementation.

### How to Handle Reviewer Comments

- Don’t Take it Personally

  - When a reviewer provides a critique of your code, think of it as their attempt to help you, the codebase, and Google, rather than as a personal attack on you or your abilities.

  - **Never respond in anger to code review comments.**

- Fix the Code

  If a reviewer says that they don’t understand something in your code,

  - Your first response should be to clarify the code itself.

  - If the code can’t be clarified, add a code comment that explains why the code is there.

  - If a comment seems pointless, only then should your response be an explanation in the code review tool.

- Think for Yourself

  **No matter how certain you are**, take a moment to step back and consider if the reviewer is providing valuable feedback that will help the codebase and Google. Your first question to yourself should always be, "**Is the reviewer correct?**"

  - If you can’t answer that question, it’s likely the reviewer needs to clarify their comments.

  - If you _have_ considered it and you still think you’re right, feel free to respond with an explanation of why your method of doing things is better for the codebase, users, and/or Google. Often, reviewers are actually providing _suggestions_ and they want you to think for yourself about what’s best.

- Resolving Conflicts

  See The Standard of Code Review, which gives principles to follow in such a situation.
