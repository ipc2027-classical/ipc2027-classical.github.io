# International Planning Competition 2027 Classical Tracks

This is the website for the classical (sequential, deterministic) track of the
[IPC 2027](https://ipc2027.github.io).
This is the 11th IPC containing classical tracks making it the oldest part of
IPC.

## Calls
Please forward the following calls to all interested parties.

 - [Call for Domains](calls/ipc2027-call-for-domains.txt)
 - [Call for Participation](calls/ipc2027-call-for-participation.txt)

## Preliminary Schedule

| Event                                         | Date               |
|:----------------------------------------------|:-------------------|
| Call for domains                              | September 14, 2026 |
| Call for participation                        | November 2026      |
| Domain submission deadline                    | early 2027         |
| Planner registration                          | early 2027         |
| Feature stop (final planner submission)       | March-April 2027   |
| Planner Abstract submission deadline          | May 2027           |
| Contest run                                   | May - June, 2027   |
| Results announced                             | ICAPS 2027         |


## Tracks

IPC 2027 features four tracks: *optimal* and *agile* recur from previous
competitions; *plan-improvement* puts a twist on the former *satisficing* track;
and *hard-to-ground* is new by popular demand.

### Optimal Track
 - single CPU core
 - no internet access
 - 8GB memory limit
 - 30min time limit
 - plans must be optimal
 - The score of a planner is the number of solved tasks.
 - If a suboptimal or invalid plan is returned, all tasks in the domain are
   counted as unsolved.
 - If that happens in more than one domain, the entry is disqualified.

### Agile Track
 - single CPU core
 - no internet access
 - 8GB memory limit
 - 5min time limit
 - The cost of the discovered plan is ignored, only the CPU time to discover a
   plan is counted.
 - The score of a planner on a solved task is 1 if the task was solved within 1
   second and 0 if the task was not solved within the resource limits. If the
   task was solved in T seconds (1s ≤ T ≤ 300s) then its score is 1 -
   log(T)/log(300). The score on an unsolved task is 0. The score of a planner
   is the sum of its scores for all tasks.
 - If an invalid plan is returned, all tasks in the domain are counted as
   unsolved.
 - If that happens in more than one domain, the entry is disqualified.

### Plan-improvement Track
 - single CPU core
 - no internet access
 - 8GB memory limit
 - 30min time limit
 - An initial plan is provided for each task as a file with the extension
   `.plan` containing a list of grounded actions, as it could be used as input
   for [VAL](https:://github/KCL-Planning/VAL) (see
   [this example](plan-improvement-example.zip) for `gripper/prob01.pddl`).
 - Planners must return a plan of strictly lower cost.
 - The score of a planner on a solved task is 0 if the reported plan has higher
   or equal cost than the initial plan. Otherwise, a plan of cost C scores
   log(G/C)/log(G/C\*) where G is the cost of the initial plan and C\* the cost
   of the best known plan. The score on an unsolved task is 0. The score of a
   planner is the sum of its scores for all tasks.
 - If an invalid plan is returned, all tasks in the domain are counted as
   unsolved.
 - If that happens in more than one domain, the entry is disqualified.

### Hard-to-ground Track
 - single CPU core
 - no internet access
 - 8GB memory limit
 - 30min time limit
 - The score of a planner on a solved task is C\*/C, where C is the cost of the
   reported plan and C\* is the cost of the best known plan. The score on an
   unsolved task is 0. The score of a planner is the sum of its scores for all
   tasks.
 - If an invalid plan is returned, all tasks in the domain are counted as
   unsolved.
 - If that happens in more than one domain, the entry is disqualified.


## PDDL Fragment
IPC 2027 will use a subset of PDDL 3.1, as done since IPC 2011. Planners must
support the subset of the language involving STRIPS, action costs, negative
preconditions, and conditional effects (possibly in combination with forall,
as in IPC 2014, 2018 and 2023). We will also consider including domains with
disjunctive preconditions and existential quantifiers.

## Registration
Registration is not yet open. To register a team, you will need to provide the
following information:
1. names of participants,
2. e-mail contacts,
3. github usernames,
4. the number of repositories (code bases) the team needs (multiple
   planners can be built from the same repository),
5. a (tentative) list of tracks, where the team intends to submit their
   planners; if you are interested in a different track than optimal, agile,
   plan-improvement, or hard-to-ground, please, let us know too.
6. if applicable, a list of closed-source dependencies (e.g., CPLEX)

Based on that, we will create private repositories under the
[ipc2027-classical](https://github.com/ipc2027-classical) organization and add
all participants as users with with write access and participants can commit
to the repository as they wish until the “feature stop” deadline.

> [!IMPORTANT]
> A team can enter multiple planners into the competition, but each planner must
> have a designated first author. Across teams, each participant can be first
> author of at most one planner per track (i.e., one can be first author of
> planners of different teams if these planners participate in different
> tracks).

## Planner Submission

As in previous editions, the competitors must submit the source code of their
planners that will be run by the organizers on the actual competition
domains/problems, unknown to the competitors until this time. This way no
fine-tuning of the planners will be possible.

As in the previous IPC 2023, we will use the container technology Apptainer
(formerly known as Singularity) to promote reproducibility and help with
compilation issues that have caused problems in the past. For each team, we will
host a Github repository under the ipc2027-classical organization. We keep these
repositories private until the end of the competition when we make them public,
i.e., after the competition is concluded, we plan to make all planners, domains,
and all related data accessible from one place.

In each repository, we only consider the branch `ipc2027-classical`. Feel free
to use other branches for development as you wish, but we will ignore them. Any
file called `Apptainer.<shortname>` in the root directory of this branch defines
one entry. For the `<shortname>`, please use the name and variant of your
planner as a short identifier (a single word, up to 16 characters long, starting
with a letter, using only letters, digits, and underscores). If you build
different versions of your planner from the same repository, use a different
`<shortname>` per version. A single entry can participate in multiple tracks,
see “Apptainer Images” for details.

In previous IPCs, there were many registrations and in particular many
registrations with multiple submissions in a team. To keep the computation time
manageable, each participant can be first author of at most one planner per
track (across all teams they participate in). As in previous years, we also
request teams to submit planner abstracts describing their submissions. Planners
that are closely related (e.g., one core idea but executed slightly differently
in different tracks) can be described in a single planner abstract, but in
principle each competition entry is expected to have its own planner abstract.


## Apptainer Images

The IPC 2023 organizers prepared a [demo
submission](https://github.com/ipc2023-classical/submission-demo)
that showcases how to set up the repository and Apptainer scripts. We will
likely stick to this setup or only do minor modifications for IPC 2027.

Your Apptainer recipe files have to specify the following labels:
 * `Name`: name of the planner
 * `Description`: a short description of your planner
 * `Authors`: a list of authors, including contact email addresses (`Firstname
   Lastname <firstname.lastname@email.example>`; the first name in this list is
   counted as the designated first author)
 * `License`: the license under which you publish this code. It has to be
   permissive enough to allow us to publish the code after the competition.
 * `Tracks`: a comma-separated list of tracks this image should participate in.
   Use only the following terms to identify tracks: `optimal`, `agile`,
   `plan-improvement`, and `hard-to-ground`. For example, to run your planner in
   the optimal and agile track use
   `Tracks optimal, agile`.
 * Your Apptainer recipe must contain all of the following labels describing
   supported PDDL features. Each label must be set to either `yes` or `no`, or
   if the feature is supported only partially, then set it to `partially, `
   followed by the description of what is and isn't supported:
   * `SupportsDerivedPredicates`: specify whether your planner supports
     `(:derived ...)` construct
   * `SupportsUniversallyQuantifiedPreconditions`: `(forall ...)` in actions'
     preconditions
   * `SupportsExistentiallyQuantifiedPreconditions`: `(exists ...)` in actions'
     preconditions
   * `SupportsUniversallyQuantifiedEffects`: `(forall ...)` in actions' effects
   * `SupportsNegativePreconditions`: `(not (...))` in actions' preconditions
   * `SupportsEqualityPreconditions`: `(= ?x obj1)`, for action parameter `?x`
     and constant `obj1`, in actions' preconditions
   * `SupportsInequalityPreconditions`: `(not (= ?x ?y))` or `(not (= ?x
     obj1))`, for action parameters `?x` and `?y`, and constant `obj1`, in
     actions' preconditions
   * `SupportsConditionalEffects`: `(when ...)` in actions' effects
   * `SupportsImplyPreconditions`: `(imply ...)` in actions' preconditions

To improve reproducibility, we require Apptainer images to be self-contained and
licensed appropriately.

 * The recipe should copy the content of the repository into the container at
   the start of the build. In particular, do not clone repositories in the
   recipe.

 * If you use third-party libraries, either install them through standard
   package managers (apt, yum, pip), or copy them into the repository. Please do
   not use git submodules to include dependencies.

 * If possible, use explicit versions. For example, do not use `ubuntu:latest`
   as your base image but pick a specific version. If you install packages
   through pip, pick specific versions of those packages.

 * If your build depends on closed-source libraries that require a license,
   please contact us.

 * If you use a portfolio of existing planners, it is up to you to get
   permission from the authors of the portfolio components and give appropriate
   credit and licensing. We recommend contacting the planner authors.

In addition to reproducibility and licensing issues, we ask that you make your
image as small as possible using the following tricks:

 * Use a [multi-stage
   build](https://apptainer.org/docs/user/latest/definition_files.html#multi-stage-builds)
   where one stage is used for compiling the planner and one for running the
   planner. Copy the compiled planner from the first stage to the second, and
   only copy/install the files that are required at runtime. The size of the
   compilation stage then does not matter and the second stage can be limited to
   contain only essential files.

 * [Strip binaries](https://www.man7.org/linux/man-pages/man1/strip.1.html)
   after compilation

 * Use small packages. For example, use python-minimal instead of python if
   possible.


## Bug-fixing Policy

When a competition team registers (see above), we create a private repository
(or multiple repositories if needed) and add competitors as users with write
access. After the “feature stop” deadline, we allow competitors to send only a
pull request with bug fixes. We will review every pull request with its
accompanying description of the bug fix to make sure that no big changes or
parameter tuning is committed to the repository.

To help us with the debugging process, planner authors will be responsible for
detecting if the run of their planner and our analysis of the results was
successful. After the feature stop deadline, we will run all planners on a
representative set of tasks from the competition and give the participants
access to the results of their planners. For each run, the data will contain the
log files of the planner, measured time and memory consumption, exit code, and
our conclusion about what this means in terms of solving the instance. We ask
participants to check their results for any errors. If an error was caused by a
bug in the planner, please send a pull request on Github with a detailed
description of the bug and the fix. If the error was on our side (e.g.,
malformed PDDL) let us know as soon as possible. We plan to do one or two rounds
of this starting after the “feature stop” deadline.


## Planner Abstract Submission

All competitors must submit an abstract (max. 300 words) and an up to 8-page
paper describing their planners. After the competition we ask the participants
to analyze the results of their planner and submit an extended version of their
paper. An important requirement for IPC 2027 competitors is to give the
organizers the right to post their paper and the source code of their planners
on the official IPC 2027 web site, and the source code of submitted planners
must be released under a license allowing free non-commercial use.


## Miscellaneous

### On the Rationale behind the Plan Improvement Track

This year, we introduce a new track on plan improvement, which aims at finding a
plan that is better than a given (suboptimal) plan within the available hardware
resources. The track is run instead of the satisficing track, whose goal is to
find the best possible plan within the given resources, but without an existing
plan as input.

While at first glance this may appear to replace the satisficing track, this is
by no means the intention. We believe that this track is a generalization, as it
allows satisficing approaches to participate simply by ignoring the additional
input. More importantly, it also provides a home for other approaches, such as
those that explicitly account for a given upper cost bound or directly focus on
plan improvement, allowing them to meaningfully participate in the IPC.

Finally, this setting also provides a natural connection to recent advances in
machine learning approaches for planning, which often produce long or expensive
solutions that can benefit from subsequent plan improvement.


## Organizers
 - [Clemens Büchner](http://ai.cs.unibas.ch/people/buechner/index.html) (University of Basel)
 - [Daniel Gnad](https://fip.ifi.uni-heidelberg.de) (Heidelberg University \& Linköping University)
 - [Arnaud Lequen](https://mrlab.ai/arnaud-lequen/) (Linköping University)
 - [David Speck](http://ai.cs.unibas.ch/people/speck/index.html) (University of Basel)

Contact us: [ipc2027-classical@googlegroups.com](mailto:ipc2027-classical@googlegroups.com)
