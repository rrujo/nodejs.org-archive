# Minutes for the Node.js core team meeting of 05/07/2015

## Participants

* Alexis Campailla
* Colin Ihrig
* James Snell
* Julien Gilli
* Michael Dawson
* Robert Kowalski


## Discussions

### Upcoming releases: v0.12.3 and v0.10.39

Julien: We should release 0.10.39 and 0.12.3 next week. A few important issues
affecting many users.

#### npm upgrade to 2.8.4
Julien:
Current npm version (2.7.4) is broken for a lot of users. npm 2.8.4 fixes a
lot of issues.
The reason why we didn't catch it, the current makefile doesn't trigger an
error if you don't have CouchDB installed. It just gives a warning, that's
easy to miss.


Going to open a PR to make sure we catch these issues.

Michael:
Made some progress on Jenkins job that runs npm tests. Currently passes
only on OSX. I'll keep working on it.

Julien:
CouchDB is the server for the npm registry. There are some tests that perform
requests to CouchDB. If not installed, the tests don't run.
CouchDB needs to be installed on each of the Jenkins machines.

#### Latest libuv release (1.5.0)

Julien:
Will review changes to see if there are any important fixes, or changes to
the API/ABI, to determine if we want this in the next release.


#### Other PRs for the upcoming release

Julien: Identified 5 different PRs that we could land before the release.
Most of them already reviewed, we can land them pretty soon.
https://github.com/joyent/node/pull/8875
https://github.com/joyent/node/pull/9448
https://github.com/joyent/node/issues/25137
https://github.com/joyent/node/pull/25100
https://github.com/joyent/node/pull/14193

Another issue was with inconsistency of styles of invocations of makeCallback.
Trevor working on it. Might not make it for the next 0.12 release.

#### RC4 deprecation
James, Julien:
Need to address the problem if cyphers is undefined or null.
Need to do a last pass on the pull request, to review tests/documentation.
If we can nail this by end of week, we could make the next release next Tuesday.
If we can't land the RC4 fixes, maybe we should revert the existing fixes for
now. And do the release. And make the RC4 fixes in the next release.

James: we should be able to finish the work this week.
If delayed just a day, we'll wait.


#### More release discussions
Alexis: motivation for urgency?

Julien: 
- v8 lateral upgrade. A lot of impact on users. 
  https://github.com/joyent/node/pull/18206 
- Fixes on freeBSD
  https://github.com/joyent/node/pull/14819
  https://github.com/joyent/node/issues/8540

Colin: can we land this too? https://github.com/joyent/node/pull/9159

Michael: Christian is away for a couple weeks. I will need to take over one of
the PRs on the list.

Julien: try to sprint until Friday. We only want to land stuff that meets the
usual quality bar.

James: once RC4 issues are fixed in 0.12, we should be able to land them in
0.10.39.

Julien: start in 0.10.39, then port to 0.12.

Julien: Alexis, your PR should be added to to the 0.10.39 milestone.
https://github.com/joyent/node/pull/25100

Julien:
For 10.39, there's also a fix for timers:
https://github.com/joyent/node/pull/17203
First fix was already reviewed. Then I submitted a simpler fix. Looking for a
second review.
It shouldn't hold up the release, but it should be pretty safe and it fixes
some annoying issues.

### Flaky tests support
Alexis: io.js removed support for flaky tests. https://github.com/iojs/io.js/pull/812
It looks like this issue might be slightly controversial.
I am guessing they thought it was a mechanism for ignoring test failures in
general, while it is only meant to support the automatic merge in
node-accept-pull-request.

Julien:
In io.js they run CI to test every pull request, but they do the merge manually.
io.js folks mentioned not been able to change the commit message as a downside
of node-accept-pull-request.

Let's communicate why it's useful.
We should definitely log issues for flaky tests.

Colin: how about policy for removing the test out of flaky -say- after a week?
Somebody has to fix it. Or it should be deleted from the tests.

Alexis, Julien: The moment we mark a test as flaky, we should open an issue
and treat it as high priority.

### Node.js API working group
Alexis: there was a request for participation in this working group. Do you
know more about the charter of this working group?

Julien:
Dan Shaw has been trying to get together a group people for a standard on what
an official Node.js API is.
Maybe to enable people to implement another runtime that is compatible with
Node.

Is the working group about the external or the internal API?

James to seek more clarifications on the email thread.

### Convergence process

Alexis: in anticipation of the convergence work, where should we make changes?
Node, io, and/or convergence repo?

James: when we do our next major release, is it going to be based on
the convergence repo? If so, that's where we should be landing the new
features.

Michael: But it won't be in stable working conditions for a while.
So until we get the CI, we still do it in Node.

If we make a change in joyent/node master, we can also port it to the
convergence repo.

Colin: what if we started cherry picking stuff to io.js?

James: that works too.

Julien: still a lot users of 0.12

James: are we going to cut new releases from joyent\node master? 

Julien: not a lot of work in master at this time.

Julien: Still waiting for io.js to vote on whether they want to merge.

James: possible alternate routes. If they choose not to come into the
foundation, we can still fork io.js and use it as our own converged stream.
We still need to give it some thought.

Michael: agree with Julien on deferring until io.js decision takes place.

### Triaging issues:
Julien: how to do a better job at triaging issues coming in on github.
948 issues open. A lot more coming in.
Hard to triage them all, let alone fix them.
Could we spend a little time every day to review the issues?

Michael: schedule a slot to do everything together.

Robert: using this process in CouchDB with very good results.

Robert: we are using Jira.

Alexis: increase the bandwidth by doing it in smaller groups or
individually?

Julien: good team exercise to do it together.

Robert: let's just try it for a few weeks and see how it goes.

Julien: schedule something just to try it out, see if it works.

Everybody: ok :)

Alexis: we'll need to find a way to use github effectively.

Michael: I assume we can invite other people too.

Julien: it's also a good way to onboard additional contributors.

Schedule first meeting with existing collaborators. And if it works, we can
extend it to more collaborators.

Julien: any volunteers to lead this? If not I'll do it.

Julien: maybe we can use Slack?

Alexis: I vote for slack.

Colin: +1 for Slack.
