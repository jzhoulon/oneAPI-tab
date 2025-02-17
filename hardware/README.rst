===================================
oneAPI Community Forum Hardware SIG
===================================

The Hardware SIG hosts discussions and presentations focused on
how to enable a broad range of hardware architectures. The
oneAPI specification defines the "Level Zero" interface that
defines a hardware interface and recent discussions have also
covered a new Unified Runtime proposal.

The Hardware SIG is led by Alastair Murray (Codeplay) and Will Damon (Intel).

To find out how to join the Hardware SIG `get in touch. <https://www.oneapi.io/community/>`__

Meeting Notes
=============

2022-11-3
=========

Agenda
------

* oneAPI Community Forum, Rod Burns
* Unfified Runtime Update, Ben Ashbaugh

Attendees
---------

.. list-table::

   * - Robert Cohn, Intel
     - Alastair Murray, Codeplay
     - Jaime Arteaga Molina, Intel
   * - Ben Ashbaugh, Intel
     - Benie
     - Brice Goglin
   * - Will Damon, Intel
     - Jeff Scheel, RISC-V International
     - Juan Fumero, Univ. of Manchester
   * - Cheol Kim, Intel
     - Russell Mcguire, Intel
     - Servesh Muralidharan, Argonne
   * - Rod Burns, Codeplay
     - Romain Dolbeau, SiPearl
     - Ronan Keryell, Xilinx Labs
   * - Brice Videau, Argonne
     - Zack Waters, Intel
     -

oneAPI Coummunity Forum
-----------------------

* TABs changing to SIGs

  * separates technical discussion from formal spec work
  * working groups formed to develop spec
  * SIGs influence specifications and implementations

* Q&A

  Q: How does community feedback flow into SIGs? Show arrows where
  feeback flows.

Unfified Runtime Update
-----------------------

* Recap

  * Problem: Duplication of functionality between language runtimes
  * Proposal: Unified runtime, usable by multiple language runtimes
    and sits of multiple device APIs
  * Feedback: Why not build on opencl 3.0

* Goals of Unified Runtime

  * Need glue layer between runtimes and device API. Do not need
    standard.
  * Efficiency, ease-of-use
  * Interoperability and access to native backend
  * tool and debug support
  * wide engagement by open source community
  * 2023:Q3 first production release

* Updates

  * Continue development
  * open source project, not competing standard
  * 1st class support for OpenCL

* Why not OpenCL 3.0? Concers about ...

  * Vendor support for optional OpenCL 3.0 standard functionality
  * Composability with existing code targeting non-OpenCL APIs
  * Fragmenting the OpenCL ecosystem with non-conformant layered
    implementations
  * performance and complexity of layered functionality
  * access to cutting-edge vendor specific features

  Q: Why not address above with extensions?

     Not possible for Q3:2023 target. Interesting to look at for
     something later.

* Feedback from OpenCL Working Group

  * Do similar libraries already exist? e.g. libomptarget

    * very openmp-specific

  * Can we have a vulkan unified runtime adapter

    * sounds interesting. technically possible, no current plans
    * will require extensions to Vulkan or Unified Runtime. TBD

* Q&A

  * Q: What is relation to oneAPI specification?

    Considering whether to publish as open source documentation or
    spec

  * Will this be useful to language runtime developers?

    It is something that we wanted.


  * What about device API developers? Thoughts on what should be
    exposed...

  * Tornado already has a common runtime. Why drop it and adopt
    unified runtime.

    If you already have something that works, then maybe
    nothing. Unified runtime may support additional devices, will be
    used in multiple products and battle tested.


2022-9-15
=========

Agenda
------

* Unified Runtime direction discussion (Mike Voss, Intel)
* Wrap-up

Attendees
---------

.. list-table::

   * - Ben Ashbaugh, Intel
     - Jaime Arteaga Molina, Intel
     - Kenneth Benzie (Benie), Codeplay
   * - Ronan Keryell, Xilinx Labs
     - Maria Garzaran, Intel
     - Xinmin Tian, Intel
   * - Mike Voss, Intel
     - Rod Burns, Codeplay
     - Juan Fumero, Univ. of Manchester
   * - Paul Petersen, Intel
     - Neil Spruit, Intel
     - Jianxin Xiong, Intel
   * - Alison Richards, Intel
     - Jatin Chaudhary, Codeplay
     - Gordon Brown, Codeplay
   * - Sergey Maslov, Intel
     - Servesh Muralidharan, Argonne
     - Brice Videau, Argonne
   * - Jack Frankland, Codeplay
     - Alex Wells, Intel
     - Gregory Lueck, Intel
   * - Alexia Ingerson, Intel
     - Paulius Velesko, Argonne
     - Pekka Jaaskelainen, Intel
   * - Romain Dolbeau, SiPearl
     - Brandon Yates, Intel
     - Kevin Harms, Argonne
   * - Cheol Kim, Intel
     - Tim Besard, Julia Computing
     -

Unified Runtime Direction Discussion
------------------------------------

`Slides <presentations/Level-Zero-Spec-v1.5.pdf>`__

* Problem statement: all-to-all connection between language runtimes
  and driver backends.

* Pros and Cons for each approach:

  * Unified Runtime as an Independent API

    * Can more quickly and flexibly evolve
    * Existing oneAPI SYCL plugins can easily be moved from PI to UR
    * Can ignore features not needed by oneAPI apps and middleware
    * There is no existing community, cannot leverage mature spec.
    * Likely perceived as not as open

  * Unified Runtime as OpenCL 3.0 Subset plus Extensions

    * Perceived as more open, many OpenCL drivers that we can leverage
    * Can leverage existing community and spec. as well as directly
      leverage existing OpenCL drivers
    * Will likely need differential spec and fork of CTS
    * Would bring in potentially unnecessary features
    * Process might be longer as the community is not small.
      OpenCL3.0 – need to evolve the standard in its community
    * Difficult to build on top of native APIs such as CUDA in a way
      that is conformant with OpenCL to specification

  * Discussion

    * Brice

      * Lack of interop and access to native backends is not a real
        issue but a simple extension to write.  There would be no
        problem starting as a vendor extension and then moving through
        the process.  Would also benefit other layered implementations
        such as those from POCL or layering over Vulkan, Metal, …
      * Looking at the current draft of the Unified Runtime, pretty
        much the entire OpenCL spec is already there.
      * Some implementations may not be conformant?  Defer to POCL.
        But even if it's not conformant on all devices may not be a
        show-stopper, doesn't need to be a goal.  Non-conformance can
        be measured by the CTS suite so we will know what is and is
        not conformant.
      * Real question: Do you need to evolve the OpenCL specification
        in a significant way?  If so, this would be good feedback into
        the OpenCL working group.  Already being discussed for other
        layering.

    * Paul:

      * We can’t just focus on functionality, but also need to think
        about performance with application with native backend – a
        goal is not to lose the overhead through a Unified Runtime.
      * Mike: Do we have differences in the execution model between
        e.g. OpenCL and CUDA?  Examples: events.
      * Pekka: Echoed a lot of what Brice said.  OpenCL implementation
        would involve exposing OpenCL layer to upper layer;
        categorizing the extension as OpenCL 3.0 mandatory to support
        upper layer.  OpenCL performance test should be required as
        well.

    * Ronan

      * Do we have a problem of supporting all of the features we want
        through OpenCL?  What about e.g. USM?
      * Pekka: This is why we have extensions.  Ideally we are at
        least functional via standard features and only need
        extensions to go faster, but we may need required extensions
        at least for now.
      * Ronan: You should give this presentation at the Khronos OpenCL
        f2f!  Good feedback to the OpenCL community.
      * Pekka said that it’d be a truly open standard
        approach...agreed with Ronan.

    * Gordon

      * Many differences can be resolved with extensions, but not all.
        Sometimes there are design choice difference vs. omissions.
        Example: Images, Contexts, Events
      * CUDA has a different way to map the images (1 to 1 mapping if
        you will) and handle events…quite different execution models.
        Might cause some performance issue.

    * Benie:

      * If there is an application that has a lot of CUDA code already
        and wants to move to oneAPI you really want a way to migrate
        to oneAPI that enables reusing a lot of the existing CUDA
        code.  This implies that you do not want to build upon the
        native NVIDIA OpenCL driver, which does not layer on top of
        CUDA (that we know of).

    * Juan Fumero:

      * How does Level Zero fit into this?
      * Answer: Level Zero will still exist.
      * Concern: Not only for native applications, also for managed
        runtime applications: python, java, julia, etc.  Need OpenCL
        to catch up with function pointers, unified memory, etc.
        Would be good to enumerate which extensions are needed to
        close gaps.
      * Brice: Not sure what the concern is?  The OpenCL language to
        describe kernels, or the runtime APIs?  We still need more
        discussion around the concern.
      * Juan: What about the functionality that OpenCL offers?  Things
        like garbage collection.  Level Zero solves some of the
        problems.

    * Kevin Harms:

      * Rather than looking at pros and cons, it might be better to go
        back to original goal/objective.  Outline/objective should be
        clear.  OpenCL 3.0 is a good fit or not…then we should discuss
        why and why not.  Would be good to be back to basic.  Not
        going to argue for one vs. the other, more trying to outline a
        decision process.

* Wrap-up

  * Agreed to looking for the opportunity to communicate with Khronos
    OpenCL WG and making sure to have a better idea on what we should
    do.

  * Agreed to discuss more on the Unified Runtime direction at the
    next TAB meeting.


2022-8-18
=========

Agenda
------

.. list-table::

  * - Topic
    - Presenter
  * - What is in Level Zero v1.5?
    - Jaime Arteaga Molina
  * - Unified Runtime
    - Zack Waters

Attendees
---------

.. list-table::

   * - Ben Ashbaugh, Intel
     - Alastair Murray, Codeplay
     - Jaime Arteaga, Intel
   * - Kenneth Benzie (Benie), Codeplay
     - Brice Goglin
     - Arlin Davis, Intel
   * - Ravi Ganapathi, Intel
     - Gordon Brown, Codeplay
     - Kevin Harms, Argonne
   * - Hugh Delaney, Codeplay
     - Jack Kirk, Codeplay
     - Jeff Scheel, RISC-V International
   * - Juan Fumero, Univ. of Manchester
     - Ronan Keryell, AMD Xilinx
     - Cheol Kim, Intel
   * - Greg Lueck, Intel
     - Sergey Maslov, Intel
     - Mehdi Goli, Codeplay
   * - Steena Monteiro, Intel
     - Servesh Muralidharan, Argonne
     - Nicolas Miller, Codeplay
   * - Paolo Gorlani, Codeplay
     - Paulius Velesko
     - Paul Petersen, Intel
   * - Romain Dolbeau, SiPearl
     - Tadej Giglaric,
     - Xinmin Tian, Intel
   * - Tim Besard, Julia Computing
     - Peng Tu, Intel
     - Victor Lumuller, Codeplay
   * - Brice Videau, Argonne
     - Michael Voss, Intel
     - Zack Waters, Intel
   * - Brandon Yates, Intel
     - Ravindra Babu Ganapathi, Intel
     - Russell Mcguire, Intel


Level Zero v1.5
---------------

`Slides <presentations/Level-Zero-Spec-v1.5.pdf>`__

* Reviewing Public Issues for Level Zero v1.5
* Top issue: #7, improving the interaction of sysman and the core
  APIs, remove environment variable.

  * Servesh: Is there a way in the API to determine what can and
    cannot be done?  Basically, can we define what you can and cannot
    do as an unprivileged user?

    * Jaime: Is this an implementation detail?
    * Zack: We should define a return value for insufficient permissions.
    * Jaime: We already have this return value.
    * Servesh: Usage model is that you need to perform a series of
      calls and want to know if they will succeed.
    * Suggest filing an issue for discussion.

  * Also: #11, Device and metric timestamp synchronization.
  * Remainder are documentation updates:

    * #6, Add IPC support for host allocations.

      * Jaime: Note, this doesn't include support for shared
        allocations, only adds support for host allocations.

    * #8, Clarify that a context created against a root device
      automatically includes all of its sub-devices.

      * Purely documentation, driver is already behaving this way.

    * #9, Allowing IPC events with timestamp events.

      * Can't think of a reason to disallow this.

  * Jaime: Are there any other must-fix issues for v1.5?
  * Brice: It would be easiest to add a GitHub milestone for these
    issues, for tracking.
  * There are a few other issues that have come in recently, but they
    may not make v1.5:

    * #12, deprecated power limits APIs.
    * #5, consider extending event states beyond 2?
    * #13, callback when Level Zero frees memory.

      * Peng: Good direction to make this more general.  Another
        request is to indicate when Level Zero is finished with a
        command list.

  * All the issues have been posted on the Level Zero GitHub; we’d
    appreciate for your feedback and input.
  * Timeline:

    * Targeting a release candidate in September.
    * Targeting release in October.

  * Github spec source walkthrough (Zack).
  * Ronan: As a general question, are you looking at all at embedded
    or safety critical applications?  Note that things like callbacks
    are forbidden in safety critical contexts.

    * Zack: Many features are optional since not all devices support
      every feature, so perhaps an embedded device might not support
      callbacks.

  * Brice: How do you plan to handle removal of experimental
    extensions or promotion of experimental extensions to standard
    extensions or core features?  Specifically looking at symbols in
    the loader and entries in the DDI table.

    * Brandon: We can't remove anything from the dispatch tables, need
      to maintain backwards compatibility.
    * Jaime: At least, we need to keep the symbols until the next
      major version.
    * Zack: We do allow experimental extensions to change things like
      the function signature.  Does this cause a problem for the
      loader?
    * Brice: Yes, it could.
    * Zack: Maybe we need to do something differently for experimental
      extensions then.

Unified Runtime
---------------

* Walked through the posted Unified Runtime ver.0.5 specification.
* Reviewed the overview and objective: Intro - Unified Runtime API for
  interface for Parallel Language Runtimes such as Julia etc.  Unified
  Runtime API enumerates Open CL, ROCm, CUDA, and others through the
  API.  Runtime is extensible - new support platform with platforms;
  new functionalities, some features that CUDA and Open CL provide.
  We have ability for platform extensions with Unified Runtime API.
  Extension interfaces provide native access to the platforms - Open
  CL, CL objects, etc.  We want the Runtime easier to be used.
* Fundamentals - overview of API designs; repo will be coming soon;
  working on it with Legal.  Naming convention: zer for now, other
  conventions in the future.
* Multithreading and concurrency; overall ABI - backward compatibility
  requirement stated on the spec.
* Programming guide - API documentations that state structures,
  descriptions, etc.  Platforms represent a collection of physical
  devices in the system accessed by the same driver.
* Queue and Enqueue: how to take the kernels and launch the device; A
  queue object represents a logic input stream to a device
* Native driver access - a set of APIs provide accessors for native
  handles.  We can leverage a platform extensions to convert the
  native handle to a driver handle. Given a zer_program_handle_t
* Brice: Somebody copy-pasted OpenCL.  Why not just use OpenCL?  Each
  of the APIs is basically the exact equivalent of OpenCL.

  * Zack: Want to evolve more towards Level Zero.  Started with what
    we have for SYCL.
  * Servesh: Maybe a different question.  What is the added value
    vs. calling Level Zero or OpenCL?
  * Brice: The added value is bring back everything that was stripped
    from OpenCL in Level Zero.

* Kevin Harms: Suggest updating the top-level document to add an
  application.  Would the expectation be that an application only
  calls through the parallel language runtime?  Or could it (would
  it?) directly interface with the unified runtime?

  * Paul: We expect that most applications will call through a
    parallel language runtime, but it is a layered architecture and
    applications can call into the lower levels if desired.
  * Jeff (RISC-V): Availability is key.
  * Jeff: The advantage is less for existing applications that are
    already programming towards the lower-level layers, and more for
    the next application that can take advantage of hardware that they
    may not otherwise.

* Kevin: Will the Intel OpenMP adopt the Unified Runtime API?

  * Paul: Yes, especially for accelerator offload.  The OpenMP
    libtarget API would target the unified runtime rather than Level
    Zero.

* Gordon: Is there a long-term goal to improve interoperability if
  SYCL and OpenMP both layer on the unified runtime?

  * aul: Yes.  Provides an opportunity to share the same abstractions.

* Juan Fumero: Is the input always SPIR-V?  How will this work for
  CUDA?  Could it be PTX IL instead?


2022-6-9
========

Agenda
------

.. list-table::

  * - Topic
    - Presenter
    - Time
  * - `Intro about Level Zero TAB & Roadmap`_
    - Paul Petersen, Intel
    - 20 min
  * - `Level Zero Specification & How to Participate`_
    - Zack Waters, Intel
    - 20 min
  * - `Discussion Topic:  Separation of Sysman from core Level Zero APIs`_
    - Ben Ashbaugh, Intel
    - 20 min
  * - Wrap up, Question & Answer
    - All
    - 10 min


Attendees
---------

.. list-table::

   * - Robert Cohn, Intel
     - Alastair Murray, Codeplay
     - Jaime Arteaga Molina, Intel
   * - Ben Ashbaugh, Intel
     - Benie, Codeplay
     - Brice Goglin
   * - Arlin Davis, Intel
     - En Shao (ICT)
     - Ravindra Babu Ganapathi, Intel
   * - Alexia Ingerson, Intel
     - Juan Fumero, University of Manchester
     - Rahul Khanna, Intel
   * - Cheol Kim, Intel
     - Sergey Maslov, Intel
     - Michal Mrozek, Intel
   * - Servesh Muralidharan, Argonne
     - Paul Petersen, Intel
     - Raja Apphuswamy, EURECOM
   * - Laura Reznikov, Intel
     - Romain Dolbeau
     - Xinmin Tian, Intel
   * - Tim Besard, Julia Computing
     - Peng Tu, Intel
     - Brice Videau, Argonne
   * - Vincent Casillas
     - Michael Voss, Intel
     - Zack Waters, Intel
   * - Jianxin Xiong, Intel
     - Brandon Yates, Intel
     - Russel Mcquire, Intel
   * - Kevin Harms
     -
     -


Intro about Level Zero TAB & Roadmap
------------------------------------

`Slides <presentations/l0-tab-intro.pdf>`__

.. notes for the topic

- There is contribution guideline on the Github.
- What is the right cadence, frequency?  What kind of interest level?
  Any feedback?  oneAPI is trying to solve a difficult problem.
- LevelZero spec has been shared from beta 1.0
- Does oneAPI need a Unified Runtime?  We might want to partition?  We
  could simplify it as a hardware device layer.  Device Abstraction
  should be required.
- What is the primitive function that we have not been covering so far
  to support your fav language?
- Do we need special support for the CPU?  CPU device driver or
  resource management?  Leverage common components…memory structure
  for heterogeneous compute platforms.  Proposing Unified Runtime API.
  It's a fairly radical sw infra…relatively major change to our sw
  structure.  Revolutionary change should be required.  Need a smooth
  transition to discuss and agree the directions at TAB and other
  places.


Level Zero Specification & How to Participate
---------------------------------------------

`Slides <presentations/22ww24_LevelZeroSpec_TAB.pdf>`__

- Spec.1.4 has been published in May
- Starting with Level Zero spec. v1.5.
- Scripts generate spec and headers from API spec and programming
  guide; covering YAML, headers, implementation to make sure codes are
  compiled, and API spec.  Programming guides are validated by script.
- Trying to ensure backward compatibility: minor version increment,
  major version increment
- Next steps: release spec dev framework, post spec issues from
  internal repo, organize candidate spec update for spec v1.5.
- Pls contribute to Level Zero spec, help us evolve Level Zero, and
  propose new feature required. What Level Zero topics should be
  covered in future TAB meeting?
- What's the relationship between Implementation and spec?  Spec
  without implementation led to errors that are hard to fix. Now we
  wait for implementation before finalization. Prove out a feature as
  an extension, even if inclusion in spec is the goal.

Discussion Topic:  Separation of Sysman from core Level Zero APIs
-----------------------------------------------------------------

`Slides <presentations/22ww24_Sysman_TAB.pdf>`__

- Currently LZ Sysman is tightly coupled to LZ Core APIs, a problem is
  that it's unclear who should enable Sysman, and how and when.
- Proposal from Ben: Add a zeslnit() for initializing sysman,
  independent of zelnit(), add query functions for sysman driver and
  device support, add function to get sysman handle from coreAPI
  handle, consider enumerating sysman separately from core APIs.
- Questions from Ben: right direction?  How important is backward
  compatibility?  Do we need to separate privileged sysman form
  unprivileged sysman?  How to handle ZES-ENABLE_SYSMAN_LOW_POWER?  Do
  we need to decouple other tools as well (e.g. debugging)?
- Servesh - how will we separate Sysman from the Core?  We'd enable
  decouple…but answer is it all depends.
- Peng Tu - will it make easier for a developer to enable Level Zero
  in that way?  Currently most SYCL users don't use Sysman, so we
  still need more feedback.
- Brice Videau (from Argonne) - Agree.  this is only way…decoupling is
  a good idea.
- Juan (from Manchester) - Running different version should be ok?
  Implementation details.  Interchanging devices.
- Why do we need to initialize Sysman?  We want the architecture to be
  able to initialize separately.  You need a specific dependency.  The
  right flow is to check the dependency and initialize Sysman.  It's
  more like requirement.
- Servesh: It seems like the target is for accelerators…future is
  device sitting in CPU and other devices probably.  Have you thought
  about supporting the demand for those?  We'll make sure that ver 2.0
  would be refactoring some functionality to cover such heterogeneous
  platform support requirement.  Specs will be evolved but when?  Not
  this year…but next few years.  Need to be more flexible for
  supporting heterogeneous environment.  What's the philosophy behind
  Level Zero?  Level Zero needs to be visible so developers can
  flexibly define another abstraction layer higher as needed while
  emulating devices.  We'll need to clean up the challenge going
  forward.
- Brice Videau: What's driving Level Zero ver 2.0?  Runtime is doing
  poor job for enabling Level Zero in general.  Need to cover some
  functionality to make it implemented effciently, but has not seen it
  on Level Zero.  Rebuilding OPEN CL---some members don't like the
  idea.  TAB is a goold place to tackle the issue.


Q: How much separation would this mean for the implementation?

Q: Will separation help me to build a smaller level zero?

   Yes, sycl does not use a lot of the features in sysman

Q: Decoupling is a good idea. Can use uuid to know if 2 devices are
   the same. This is the only solution--being able to disable sysman
   whenever we want depending on the tools.

Q: Do we need to continue supporting the environment variable?

   API could override ZES_INIT=0

Q: Could decoupling lead to different versions being used?

Q: What is the overhead of zes_init?

   Don't put them in a tight loop

Q: If you decouple debugging, separate zed_init, or use mask?

   Could go either way.

Q: Today it is accelerator focused, could be used for other
   devices. Have you looked of decomposing sets of API so that optional
   fucntionality allows it.

   We have been considering that for 2.0. Want to hear feedback about
   this topic.

Q: What is the timeframe for 2.0?

   Not this year. Maybe in the next couple years. Which means we need
   to start thinking about it now.

Q: Topic on visibility of devices/affinity mask that makes devices
   available: https://github.com/oneapi-src/level-zero-spec/issues/1

   We will be presenting a proposal. We will make it a topic for a
   future meeting.

Q: To support heterogeneity, we need something more flexible than the
   current affinity mask. Don't see clear device abstraction.

Q: Any plans to allow for vectorized representation of SPIR-V for
   front ends that already have efficient vectorized code generation?

   I think this is already supported? If it isn't, is this an
   implementation question, or a spec question? Let's focus on spec
   questions here.

Q: What should drive level 2.0? Need features to build runtimes on top
   of level zero. Runtimes use l0 inefficiently, polling, many
   threads, etc. Need async programming models. L0 should be
   sufficient or provide capability to do that on top. Seen that issue
   with hip on top of l0. Difficult to get right, error prone,
   especially multi-threading. Everybody needs to implement the same
   thing, and does a poor job. Users should not handle helper threads.

Q: Can we show that opencl API on top of L0 has same efficiency?
   People should not have to figure out tricks to get performance.
