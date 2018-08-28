Currently working on
=====================
- engineering/architecture/reviews/process for experiments program
- polishing prio integration
  - moving libprio automated tests into tree, etc.
  - helping out Telemetry folk w/ integration
- Shield Study PRD for Prio

Daily(ish) log
==============
2018-08-09 -> 2018-09-01
------------------------
- super busy the last few weeks, catching up:
  - landed libprio + PrioEncoder, shipped in Nightly \o/
    - some followup work
      - provided easy way to disable building libprio + PrioEncoder, via MOZ_LIBPRIO flag
        - hit this issue with MSVC which is tier-2 and which we will almost certainly never ship again,has an ancient C compiler (C90). Encouraging upstream to make Clang the first-class compiler, since folks like Firefox and Chromium are moving that way anyway.
          - https://bugzilla.mozilla.org/show_bug.cgi?id=1485946
        - set up travis-ci for upstream libprio, so we don't have to wait until we re-vendor the thing into Firefox to find problems.
          - https://github.com/mozilla/libprio/pull/22
      - re-implemented some ASCII-only versions of std functions like toupper/isxdigit, due to these being locale-dependent
        - https://github.com/mozilla/libprio/pull/24
      - started looking at moving the libprio (manually run) browser-test over to a proper Firefox unit test
        - https://bugzilla.mozilla.org/show_bug.cgi?id=1485620
        - asking for advice from DOM folks, thinking that we'll probably want to expose this to JS (for the xpcshell unit test runner) via some new DOM functions which are behind a test-only pref.
          - browser-test is C code that invokes xpcshell, but for Firefox what we need is for xpcshell to be able to invoke the native code.
    - passed the ball over to Telemetry folks
      - client integration should be simple, provided sample code
        - https://bugzilla.mozilla.org/show_bug.cgi?id=1465251
      - server integration + analysis probably a bit more involved, pointed to some example code there as well but likely we'll want to build some standalone tools using libprio. I don't think this should be a blocker on getting the client code shipped and starting to collect the data.
        - https://bugzilla.mozilla.org/show_bug.cgi?id=1465252
  - working on Telemetry Coverage
    - https://blog.mozilla.org/data/2018/08/20/effectively-measuring-search-in-firefox/
    - taking a bit more time than expected but trying to do it right
  - investigated problems with OpenWPM study
    - https://github.com/mozilla/OpenWPM-WebExtension-Experiment/pull/4
    - reached out to rpl and devtools folks, they just missed their GH mentions, on the case now

2018-08-09
----------
- reviewed WebCompat GoFaster extension to Fennec
  - https://phabricator.services.mozilla.com/D3012
- I *think* I've ironed out the last of the blockers for the Prio prototype landing in Firefox
  - https://bugzilla.mozilla.org/show_bug.cgi?id=1421501
  - have a good cross-platform try run now
- put up example usage of Prio for client
  - https://bugzilla.mozilla.org/show_bug.cgi?id=1465251#c7
- starting rewriting prio integration test for latest API
  - https://github.com/mozilla/libprio/issues/7
  - got some nice modern JS digs in too

2018-08-08
----------
- focused on libprio+firefox cross-platform build issues w/ help from Henry and Franziskus
- reviewed OpenWPM-WebExtension-Experiment
  - https://github.com/mozilla/OpenWPM-WebExtension-Experiment/pull/4/files
  - don't see anything concerning, will take another look tomorrow

2018-08-07
----------
- pushed new patch, few questions for DOM reviewer but feeling close now
- started working on linux/windows build problems for libprio
  - https://github.com/mozilla/libprio/issues/4
  - https://github.com/mozilla/libprio/issues/3

2018-08-06
----------
- worked through build integration problems from last friday:
  - vendored msgpack + integrated
  - used in-tree NSS mpi lib
  - need to do a few supporting changes in libprio but nothing major
  - getting further on tryserver, hitting some cross-platform issues like:
    - linux is unhappy with multiple main functions, this is because we're building an NSS mpi file that we just don't need, this can be fixed in the libprio moz.build integration in my patch
    - windows doesn't provide `<strings.h>` but does provide `<string.h>`, if that's not enough for libprio then I'll need to make some further changes but initial results on macOS (which is my primary dev environment) look good

2018-08-03
----------
- got back prio review responses
  - little more work to do on the DOM bit
  - turned up some build system integration problems (one turned up by tryserver and one found by NSS reviewer):
    - need to vendor msgpack
    - need to use in-tree private NSS mpi lib not the copy in libprio

2018-08-02
----------
- got buy-in on prio plan mentioned yesterday
  - pushed latest patches for review
    - I wasn't able to resolve some of the DOM concerns (was crashing trying to use suggested Mozilla string libraries when passing to C etc) so asked for help on those

2018-08-01
----------
- started working through Prio DOM review
  - going to try to land current approach and then follow-up with new requirements from the meeting a few weeks ago
- followed up on github mentions
  - https://github.com/mozilla/shield-studies-addon-utils/issues/254#issuecomment-408998204

2018-07-23
----------
- worked on adding ArrayBuffer support for PrioEncoder
  - this is more important now, since we're talking about sending
  way more Telemetry through.
  - getting hung up on silly issue with `nsCOMPtr<nsIGlobalObject>`
  being easily available but not the `JSContext` (which would be accessible from the global passed to the constructor via `aGlobal.Context()`).
    - this is one of those issues where it's easy to fix (keep a reference to the JS context around) but more about trying to figure out how the existing code does it so it's more likely to pass review
- responded to bug about making Normandy use ServiceRequest vs
raw fetch
  - https://bugzilla.mozilla.org/show_bug.cgi?id=1471946#c19
  - I filed this because I noticed Normandy wasn't doing NSS beConservative, since we're using it for hotfixes and we only serve signed content
  - I wrote up a patch to wrap XHR (which is what ServiceRequest is
  built on top of) but expose it with a fetch-like API, however per comment above I think we should just go a few levels deeper and
  1. expose underlying network channel from fetch to system JS
  2. expose simple fetch wrapper from `ServiceRequest.jsm` that sets all the right network channels
  3. get sec review on this

2018-07-17
----------
- back after being out w/ flu for a week
- reviewed+merged outstanding libprio PRs
  - https://github.com/rhelmer/gecko-dev/pull/2
  - https://github.com/mozilla/libprio/pull/1
- https://github.com/mozilla/libprio/ is now the official upstream \o/
- followed up on TLS 1.3 fallback-limit roll-out
  - there's a hotfix we might want to block on to make the analysis cleaner, unsure.
- emailed nika about prio review
- sought out engineering design/architecture advice

2018-07-12
----------
- responded to henry's email re: recent prio PR
- reviewed idle callback patch for nsUpateTimerManager
  - waaay simpler than I thought it was going to be
  - https://bugzil.la/1373408

2018-07-11
----------
- shipped TLS fallback limit to 25%
  - did a little telemetry notebook debugging first
- got back to henry re: hex-to-bin library
  - had looked into it last (holiday) week but not followed up yet
  - tl;dr nothing easily reusable, just utility functions in skia / nss
  - henry is going to do it in prio and expose function to import hex-encoded keys
- rebased prio client against latest m-c

2018-07-10
----------
- PTO (still out sick)

2018-07-09
----------
- pushed TLS fallback limit to release 61 at 10%
- didn't get as much done as I'd like, starting feeling sick

2018-07-06
----------
- met w/ mreid re: prio telemetry

2018-07-05
----------
- worked on prio client

2018-07-04
----------
- US holiday

2018-07-03
----------
- went to MV for meetings
- figured out plan for landing prio client

2018-06-28
----------
- prio sec review (client-side)
  - https://bugzil.la/1421501#c17
- filed bug + submitted patch for normandy to use ServiceRequest instead of raw fetch()
  - https://bugzil.la/1471946

2018-06-27
----------
- so many meetings
  - prio RRA (server side stuff mostly, little early for it)
  - telemetry for normandy pref-flip roll-outs
  - other follow up from yesterday
- kept working through review feedback for prio impl

2018-06-26
----------
- worked on review feedback for prio impl
- more meetings than usual
- investigated update history

2018-06-25
----------
- helped w/ florian's study

2018-06-22
----------
- finished reviewing new TAAR study
  - https://bugzil.la/1469546
- set up mozilla repo for libprio, so henrycg can do a PR and get NSS peer to look at it that way
  - some confusion in the bug because upstream lib has both client and server parts, would be better
  to resolve all of this in the repo, and have a mozilla-controlled upstream repo anyway
  - https://github.com/mozilla/libprio

2018-06-21
----------
- fwd'd review for libprio-specific bits to henrycg
- helped out w/ intern shield study
- reviewed shield pref flip study patch
  - https://bugzil.la/1465195
  - nothing really for me to do here
- reviewed new TAAR study
  - https://bugzil.la/1469546
- took a look w/ chutten at TLS 1.3 telemetry notebooks
- chatted w/ bdanforth about testing strategy for study extensions, ahead of test infra meeting
- met w/ intern working on prio

2018-06-20
----------
- started exploring on better experiments + firefox integration for shield study needs
- chatted w/ relman re: tls roll-out plans for next few releases
  - need to send intent-to-ship emails for next round soon
- put prio prototype patches up for review \o/
  - https://bugzil.la/1421501

2018-06-19
----------
- PTO in morning
- working on generating test private/public keypairs for this prio code so I can get it up for review
  - found it easiest to just make a little python script use libsodium for generating CURVE25519 keypairs
    - https://gist.github.com/rhelmer/3331ca166bcc9ee05c21a1834fa58cea
  - this is fine for testing purposes but will make sure the sec folks generate and handle this key as
  part of review for the version we actually ship.. can put the public key in a pref
- still working on that python telemetry notebook too
  - mythmon helped with this so now have the basic query working at least
- chatted w/ add-ons and experiments folks about upcoming shield study
  - tl;dr is that it's been prototyped as a legacy extension, I actually already chatted in person w/ folks
  last week about converting this over to bundled webext experiment, should be nbd
  - sent some docs and examples to interested folks
- reviewed patch to re-enable temporary extension unit tests on windows followin race condition fix
  - https://bugzil.la/1469686

2018-06-18
----------
- worked on python telemetry notebook for tracking TLS fallback-limit via normandy on beta
  - https://dbc-caf9527b-e073.cloud.databricks.com/#notebook/16917/command/16952
- talked w/ henry @ stanford re: prio next steps
  - henry suggested putting public key somewhere we can easily change; using a pref or passing
  to the C++ constructor would work
  - henry is working on command-line encrypt/decrypt tools for Telemetry server's use
- sent prio status to ekr's intern
  - meeting set up later in the week

2018-06-11 -> 2018-06-15
------------------------
- mozilla all-hands

2018-06-07
----------
- debugged why my local build is broken
  - some XPI generation issue, both artifact and full builds
- landed savant bug for bdanforth
  - autoland kicked back due to merge issue
  - she looked into and was an issue where hg bookmark needed to be updated
- moved my prio work from git over to hg
  - old moz-git-tools repo has a handy tool for taking a git format-patch
  output to something hg import can handle
    - https://github.com/mozilla/moz-git-tools/blob/master/git-patch-to-hg-patch

2018-06-06
----------
- talked to ursula re: split up work for prio
  - suggested reviewer for my part, contacted and lined that up
- pushed new version of TLS 1.3 roll-out to bug (for release)

2018-06-05
----------
- met about new shield utils webext experiments review
  - glind already split out commits for me, should be done reviewing today
  - meeting next week to talk about engineering, not going to sweat
  the details or block them shipping right now

2018-06-01
----------
- looked at results of beta fallback-limit push, so far so good

2018-05-30
----------
- kicked off perf+correctness testing for new shield study utils, as
  part of reviewing
  - https://treeherder.mozilla.org/#/jobs?repo=try&revision=f3d72bddf60c5ae496ed186a139644ac7cd60150
- pushed TLS 1.3 fallback-limit on release (SAO) and beta (normandy)

2018-05-29
----------
- 1:1
- filed bugs splitting up prio work, so I can land the DOM bit sooner
- helped out bdanforth w/ savant study-related questions

2018-05-28
----------
- PTO (US Holiday)

2018-05-24
----------
- reviewed bug for bdanforth's Savant shield study
  - needs to ship w/ Firefox behind a pref
- started working on testing for Fennec system add-on update bug
  - https://bugzil.la/1260213

2018-05-15
----------
- reviewed bug about divorcing SAO update from app.update.enabled pref
  - https://bugzil.la/1428459
  - second round, r+
- responded to needinfo about signing built-in extensions
- corresponding w/ henrycg about using the prio API correctly
  - I wasn't collecting all of the output from `PrioClient_encode`, getting closer
    to the expected result except the number of elements in the "forServerA" array
    is larger than "forServerB"... clarifying whether this is expected or a sign I
    am doing something wrong
- merged AES removal from libprio vendoring
  - https://github.com/rhelmer/gecko-dev/pull/1
  - fixed some merge conflicts
  - made sure that henry landed the same change in the upstream libprio github repo,
    as we're probably going to automate vendoring and checking for updates etc. in Firefox
    eventually.

2018-05-14
----------
- sent some questions from prelim review to henrycg
  - pointer ownership and cleanup questions
  - quick question about simplifying the JS API
- helped bdanforth test the easier XPI loading integration for mochitest
  - seems to work

2018-05-07
----------
- needinfo'd folks on bug about whether SAO updates should be active in safe-mode
  - https://bugzil.la/1459186
  - built-ins are not deactivated, and updates are. this was done on purpose, but
    worth reconsidering.
    - ended up wontfix'ing, not worth changing as it matches current user expectation

2018-05-04
----------
- reviewed SAO for UA override on Fennec
  - https://bugzil.la/1453691
  - patch lgtm; made some suggestions for bullet-proofing it more, like the ability
    to sync data and not require a code update just to add/remove domains/UA strings
  - needinfo'd kmag because I know he's working on some build system cleanup which
    should be reused by this, so they will either wait for him to land or take that
    part of his patch now.

2018-05-03
----------
- decided to just return array-of-arrays from `PrioEncoder.encode()` for now, since
  we're only encoding two 8-bit bytes right now. Will bring this up in code review,
  but don't think it should block testing.
- clarified the use of the release-sysaddon test channel for QA
  - https://bugzil.la/1458579
- looked into push of Google search fix SAO update, working overall but not seeing
  it in super old versions like Firefox 43
  - https://bugzil.la/1454443
  - looking into the history of system add-on feature, looks like we have built-in
    extensions working in this timeframe but not updates, so won't work for this
    version
  - pushing a classic Hotfix add-on would work if this is important enough to bother

2018-05-02
----------
- looked into why espr study isn't seeing as many pings as expected
  - wondering if it's due to a missing `await` on an `async` function that gets
    called during early return of `startup()`...
  - https://github.com/motin/esper-pioneer-shield-study/issues/26#issuecomment-386145068
- looked into sentry exception coming from activity stream
  - https://bugzil.la/1458621
- reviewed bug about moving dictionaries into the omni jar
  - https://bugzil.la/1457321
  - r+'d with a question about why this even needs to use the terrible build system
    hack I put in for system add-ons in 57 to generate a list of acceptable add-on IDs,
    versus just using the index of the JAR...

2018-04-27
----------
- hooked up error checking for PrioEncoder and pushed to github
  - promise rejects now if there's any error in underlying libprio calls
- spent the rest of the day on wrapping libprio's output in an Array of
  ArrayBuffers. Having unexpected problems with the ToJSValue() template
  

2018-04-26
----------
- figured out my libprio string problem, batchID is passed to libprio correctly now \o/
- helped bdanforth figure out where to start up their code
  - https://searchfox.org/mozilla-central/source/browser/components/nsBrowserGlue.js is probably the best place - this is per-session rather than per-window, like browser.js
  - the trick is to init after the observer notification you want is observed, ideally as late in browser startup as possible: https://developer.mozilla.org/en-US/docs/Observer_Notifications
    - by-the-by, that page would probably be a good candidate to move to https://firefox-source-docs.mozilla.org/ and use autodoc to generate

2018-04-25
----------
- attended Normandy brain-dump meeting, took notes
- put together beginning of architecture doc based on normandy notes
- chatted w/ bdanforth re: integration of the savant study
  - going to land it in-tree vs. using an extension

2018-04-24
----------
- spent most of the day trying to figure out how strings work in mozilla C++ code
  - https://developer.mozilla.org/en-US/docs/Mozilla/Tech/XPCOM/Guide/Internal_strings
  - context is needing to convert an `nsString` to `const unsigned char*` to use w/ libprio
    C code

2018-04-19
----------
- spent the morning dealing with aftermath of MBP upgrade
  - got my apple ID working and downloading xcode so I could actually build firefox locally again
- hacked on prio and reported status to group
  - imported latest prio and start working with the newest API
  - todo:
    - hooking up the right public keys
    - adding some error checking that's compatible with the way our C++/JS bindings work
    - some simple tests to make sure the integration is working
    - actually return `ArrayBuffers` in the `Promise` that `encode()` returns
      - right now it is just a pair of strings

2018-04-18
----------
- hacked on prio integration
  - henrycg pushed new version w/ some API changes that needed to be imported
  - pretty close to feature complete!
- prepared TLS 1.3 system add-on updates
  - https://bugzil.la/1448176
  - https://bugzil.la/1448176


2018-04-17
----------
- met re: updates
- attended github integration meeting
  - other than vendoring from upstream projects, mostly interested in how test integration should
    work for things like studies and system add-ons that never land in m-c but nevertheless get shipped
    to some subset of users
- reviewed re-launch of ESPR study
  - https://bugzil.la/1450951

2018-04-16
----------
- made plans re: Normandy arch docs
  - firefox-source-docs.m.o (built from m-c source) is probably the most discoverable right now
  - GH pages or google docs also an option, maybe linked from above
  - good support for diagrams (ideally something like graphviz) might make the choice for us
  - regardless of actual hosting would be ideal to have an authoritation mozilla.org URL or at least link to it from one

2018-04-11
----------
- reviewed bug cleaning up Cert.jsm exports
  - https://bugzil.la/1453123

2018-04-09
----------
- hacked on prio dom integration
  - made closer to mozilla c++ style guide
  - starting working on testing
    - adding a JS test for the `PrioEncoder` DOM method should be easy, but actually testing
      that prio is returning the right result is trickier... might just do that bit in C++
      so I can use the verification code that's already in libprio
  - upgraded MBP to high sierra, had to re-install a bunch of build tools (xcode, rust, etc)
- out most of afternoon getting iphone repaired and new cord for MBP

2018-04-05
----------
- review normandy client related bug
  - https://bugzil.la/1451911
- chatted w/ henrycg re: prio
  - libprio should do its own (de)serialization in C, so callers don't have to deal with it
    - henry suggested a few third-party libs like msgpack and flatbuffers, I think the licenses are probably OK
      - henry decided on msgpack
  - also asked henry if it's easy enough to relicense libprio as MPL 2.0 to make our legal review smoother
    - he will do so!

2018-04-03
----------
- so many meetings

2018-04-01
----------
- read PHD docs for upcoming study
- updated gradual TLS 1.3 release channel roll-out for 50%
  - https://bugzil.la/1442042
  - verified XPIs and asked relman for sign-off
- reviewed normandy pref flip
  - https://bugzil.la/1443940
- walked QA through testing the beta TLS fallback-limit (beta) pref flip
  - https://bugzil.la/1442042

2018-03-29
----------
- finished review on pioneer news study 2
  - followed up on GH issue re: browser console warnings when installing extension
    - https://github.com/mozilla/pioneer-study-online-news-2/issues/25
- needinfo'd relman on TLS 1.3 for beta
  - https://bugzil.la/1448176
- followed up w/ activitystream folks on availability of API for messaging in newtab
- worked more on prio prototype
    - turns out there's a location in-tree for chrome-only
      webidl, allows for slightly nicer webidl
    - opened a PR to wrap `extern C {}` around prio's header file, so I can get it out
      of moz code (already put this in the vendored version too)
        - https://github.com/henrycg/libprio/pull/2
    - https://github.com/mozilla/gecko-dev/compare/master...rhelmer:bug1421501-prio-prototype


2018-03-28
----------
- TLS 1.3 release channel roll-out shipped at 20%
- pretty close to an actual working prio impl now! most of the right types are wired up now,
  and the prio code actually runs when you call `.encode()`
    - https://github.com/mozilla/gecko-dev/compare/master...rhelmer:bug1421501-prio-prototype

2018-03-27
----------
- reviewed pioneer news study 2
- sent (late) intent-to-ship emails for TLS roll-outs
- asked for TLS 1.3 release roll-out to ship
- emailed about prio
  - have the actual prio code running inside the PrioEncoder DOM method now
  - https://github.com/mozilla/gecko-dev/compare/master...rhelmer:bug1421501-prio-prototype

2018-03-26
----------
- got basic Prio example working \o/
  - https://github.com/mozilla/gecko-dev/compare/master...rhelmer:bug1421501-prio-prototype
  - vendoring and linking libprio, using it from webidl impl code
  - emailed folks
- chatted w/ rdalal re: pioneer
  - chrome manifest resource:// registration removed on nightly
    - use current approach + test on unbranded builds for 59+60
    - work on webextension approach for 61
- chatted w/ rstrong re: pref flip on older Fx
  - sysaddon support first landed in 43 so might be enough, need to test
  - rstrong to file bug

2018-03-22
----------
- reviewed testing strategy for shield studies w/ bdanforth
  - we both took copious notes
    - tl;dr - we want to make dev workflow the basic github workflow -
      add-ons are developed using normal add-on tools, and the mozilla
      TaskCluster CI bits are integrated via GH webhooks etc.
      as in CircleCI/Travis
  - followup action items
    - bdanforth to set up meeting w/ jmaher and myself
      also, invite me to shield dev workflow meeting next week
    - I will contact myk melez re: github working group
      - done, will catch up on their progress and attend
- Updated TLS 1.3 release channel roll-out add-on to 10%
  - https://bugzil.la/1442042
- Created new bug to roll out TLS 1.3 fallback-limit to Beta
  - https://bugzil.la/1448176
  - this is basically the same as above, but different pref and
    targeted at Beta only. Beta already has TLS 1.3 enabled, this
    stops fallback.
- Worked a bit on Prio webidl

2018-03-21
----------
- looked into issue w/ TP study not working on restart
  - bug in Firefox (RecentWindow.jsm), appears to be fixed in 60+
    - study is running on 59
  - bdanforth changed add-on to use RecentWindow.jsm consistently
    which works around it
  - study paused while we looked at it and will be relaunched shortly

2018-03-20
----------
- followed up w/ QA re: TLS 1.3 gradual roll-out
  - put together telemetry query to track
    - https://sql.telemetry.mozilla.org/queries/52077
  - attached v5 for signing, which bumps from 1% to 5% per ekr
    - also tested, hosted and needinfo'd relman
- 1:1
  - discussed topics from TODO.md

2018-03-19
----------
- followed up w/ QA re: TLS 1.3 gradual roll-out
  - https://bugzil.la/1442042
  - shipped to release \o/
  - putting together telemetry report, both to check uptake of add-om
    and also to measure effect more directly
    - ekr has an ipython notebook from previous experiments that can be
      adapted for this purpose
      - forked https://github.com/rhelmer/telemetry_utils
- reviewed bug re: directory service overrides for add-ons manager tests
  - https://bugzil.la/1446833

2018-03-16
----------
- followed up w/ QA re: TLS 1.3 gradual roll-out
  - https://bugzil.la/1442042
  - tried shipping but no relman support available
    - also QA 
    - updated ekr on status, ETA for shipping monday
- made decision on Prio prototype
  - taking the original course - webidl

2018-03-15
----------
- followed up w/ QA re: TLS 1.3 gradual roll-out
  - https://bugzil.la/1442042
  - working correctly now
  - ekr asked if we can use 1% instead of 10% for initial roll-out,
    should be fine but will require the add-on to be modified and re-signed
  - attached new XPI to bug for testing and ping'd QA

2018-03-14
----------
- followed up w/ QA re: TLS 1.3 gradual roll-out
  - https://bugzil.la/1442042
  - full test instructions used this time
  - add-on itself works, but logic that chooses 10% of profiles
    does not seem to be working for QA when creating new profiles.
    I'll try it again myself today
- met w/ bdanforth re: final tryserver result review for TP study
  - https://github.com/biancadanforth/tracking-protection-shield-study/issues/26#issuecomment-372816318

2018-03-13
----------
- followed up w/ QA re: TLS 1.3 gradual roll-out
  - https://bugzil.la/1442042
- looked into build problems w/ bdanforth on TP study

2018-03-12
----------
- followed up w/ QA re: TLS 1.3 gradual roll-out
  - https://bugzil.la/1442042
  - need to make instructions more explicit.. maybe host on balrog test channel
- worked a bit on getting built-in add-ons into the omni jar
  - https://bugzil.la/1357205
- emailed followup re: system add-on compat to dev-firefox/platform
  - https://mail.mozilla.org/pipermail/firefox-dev/2018-March/006186.html

2018-03-09
----------
- PTO

2018-03-07
----------
- added steps for QA for TLS 1.3 gradual roll-out
  - https://bugzil.la/1442042
  - looks like we're still waiting on the pref to be rolled back on beta...
- did some testing for ulfr
- tested standalone prio
  - got building on macOS and sent PR etc.

2018-03-06
----------
- chatted w/ QA re: TLS 1.3 gradual roll-out
  - https://bugzil.la/1442042
- took a look at latest prio work

2018-03-05
----------
- packaged up XPI and put in PI request for TLS 1.3 gradual roll-out
  - https://bugzil.la/1442042
- last-minute TAAR help + review
  - went over options to exclude private browsing windows
    - specifically, *any* open browser windows, not just the most
      recently active
  - https://github.com/motin/taar-experiment-v2-shield-study/pull/18
  - https://bugzil.la/1428308
- attended TP study review meeting / demo

2018-03-02
----------
- addressed review comments on add-on for TLS 1.3 gradual roll-out
  - https://bugzil.la/1442042
  - https://github.com/mozilla/one-off-system-add-ons/pull/96
- figured out plan w/ add-on folks for moving built-in add-ons to omni jar
  - https://bugzil.la/1357205
  - going to start moving away from "system add-on" naming
    - something like "built-in"
    - updates in the future will come as normandy-installed hidden add-ons,
      again moving away from "system add-on" nomenclature
- met w/ benson
- finished up review changes on add-on for TLS 1.3 gradual roll-out
  - https://bugzil.la/1442042
  - https://github.com/mozilla/one-off-system-add-ons/pull/96

2018-03-01
----------
- worked on add-on for TLS 1.3 gradual roll-out
  - https://bugzil.la/1442042
  - https://github.com/mozilla/one-off-system-add-ons/pull/96
- attended update meeting
  - caught people up on system add-on, gmp, normandy, etc. plans
  - also mentioned ServiceRequest so folks know it exists

2018-02-28
----------
- advised prio folks on technical issues integrating w/ Firefox
  - C vs. C++, memory allocation, etc.
- filed bug for TLS 1.3 gradual roll-out
  - https://bugzil.la/1442042
- worked on exposing `fetch` interface from ServiceRequest.jsm
  - first attempt was to polyfill w/ already-subclassed XHR
    - original bug just subclasses XHR
      - https://bugzil.la/1325501
    - however, `fetch` cannot be subclassed, as it is just a function
      and not a class such as XMLHttpRequest. providing a proxy
      function which calls it is probably the way to go.

      The only problem with this is that built-in `fetch` does not
      expose the underlying network channel (for settings things such
      as conservative TLS settings), so Fetch.webidl would need to be
      modified to do so (XHR has a chrome-only mechanism for doing this)
- looked at panel issue with TP study, where it is staying open due to
  the `blur` event acting on panels as well as regular windows (panels
  are a type of `ChromeWindow`) - bdanforth is looking at how to detect
  these, so the intro panel gets closed only if users either accept
  or explicitly switch windows
  - https://github.com/biancadanforth/tracking-protection-shield-study/issues/111
  - regressed by https://github.com/biancadanforth/tracking-protection-shield-study/pull/109/files

2018-02-27
----------
- looked at window-closing panel issue on TP study
  - https://github.com/biancadanforth/tracking-protection-shield-study/issues/103
- re-investigated and commented on bug about moving built-in add-ons to omni jar
  - https://bugzil.la/1357205
- worked on wrapping fetch for ServiceRequest.jsm
  - this is so we use consistent settings for requests coming from Firefox
  - original bug just subclasses XHR
    - https://bugzil.la/1325501

2018-02-26
----------
- discussed slow roll-out for a few features w/ folks
  - normandy not ready til ~61
    - https://github.com/mozilla/normandy/projects/23
  - system add-on probably the way to go in the meantime

2018-02-23
----------
- finished review for system add-on enterprise policy
  - https://bugzil.la/1436851
- out for part of day with vet emergency
- chatted w/ tor folk re: system add-ons on fennec
  - https://bugzil.la/1440789
  - tl;dr - moz build folks would prefer a better packaging mechanism
    such as https://bugzil.la/988938
- responded to willkg question regarding hive ADI socorro fetcher
  - https://bugzil.la/1440745

2018-02-21
----------
- looked at quirk of lazy-loading in TP shield study
- reviewed one of the patches on bug about controlling system add-ons with
  enterprise policies
    - https://bugzil.la/1436851
- chatted w/ tor folks about porting legacy add-on to mobile
    - tl;dr - might be OK in the short-term, not really the right thing
      long-term. maybe either make native messaging work on mobile, or
      switch to something android-specific

2018-02-20
----------
- chatted w/ bdanforth re: final unit test failure for TP study
    - doesn't happen during manual testing
    - test only happens when WebRequest is being used
    - tl;dr - shouldn't block, but worth investigating (would be
      interesting to see if webextension using `browser.webRequest` triggers it as well)
- chatted w/ prio folks re: firefox integration
    - going to do it as a standalone library and server/client examples
    - we can either ship this inside Firefox or possibly as an add-on via shield
        - could either js-ctypes or (maybe safer) just call the standalone
        client executable

2018-02-09
----------
- chatted w/ bdanforth re: channel testing requirements for shield studies
- investigating ActivityStream's TC/github integration per Standard8

2018-02-08
----------
- solicited feedback on off-train perf/correctness testing
    - https://bugzil.la/1427858
- chatted w/ mythmon re: the taskcluster/github integration and
  testing work he did for shield-recipe-client
    - https://tools.taskcluster.net/quickstart/
    

2018-02-07
----------
- worked on email re: deprecating bootstrapped add-ons
  - r? aswan
- chatted w/ bdanforth re: tryserver
  - referred her to other folks to dig into memory leaks, not sure what
    the most expedient way to track them down is

2018-02-02
----------
- met w/ bdanforth re: tryserver results
  - tracked down why artifact builds weren't working for release branches
    - https://bugzil.la/1435403
  - looked into leaked windows and remaining perf issues
    - trying one last tweak to improve perf, some small known regressions
      are expected since this is not the same approach as the final feature
      will take

2018-02-01
----------
- gave moar explicit r+ on TAAR shield study
  - https://bugzil.la/1428308
- tested fix for browserAction + webext API bustage
  - https://bugzil.la/1434076
- put some thoughts on SAO update automated testing bug, based on bdanforth's work so far
  - https://bugzil.la/1427858

2018-01-31
----------
- super-blue-blood-moon edition
- met w/ bdanforth and figured out tryserver test plan for TP study
  - running all unit+func+perf tests
  - quickly found a few issues
    - TP study add-on makes outbound connections
    - TP study randomly picks control or treatment branches
    - bdanforth will land workarounds in hg.m.o/try for both
- prio progress
  - enough C++ implemented to compile + show up in Browser Console
    - https://github.com/mozilla/gecko-dev/compare/master...rhelmer:bug1421501-prio-prototype?expand=1
    - need to figure out constructor and show stanford folk where to plug into

2018-01-30
----------
- push meeting
- prio
  - sent quick-start Firefox+github instructions to Stanford folk
  - worked on prio webidl c++ boilerplate
- worked up SQL query for tracking system add-ons on main summary
  - https://sql.telemetry.mozilla.org/queries/4262/source#table

2018-01-27
----------
- tested and reviewed TP study
- setting up GH repo for prio
  - https://github.com/rhelmer/gecko-dev/tree/prio-proto

2018-01-26
----------
- tested and reviewed TP study
- meeting w/ stanford folks
  - rhelmer to follow up:
    - w/ NSS folks on crypto\_box and fast polynomial libs
    - set up github to collab

2018-01-25
----------
- finished testing and landing patch for system add-on updates on Fennec
    - https://bugzil.la/1260213

2018-01-24
----------
- met w/ bdanforth re: TP shield study
- put up patch for review enabling system add-on updates on Fennec
    - https://bugzil.la/1260213

2018-01-17
----------
- chatted w/ glind re: shield experiment reviews and moving to webextensions
- chatted w/ mythmon more about normandy client as Firefox component
- set up meeting w/ bdanforth re: tracking protection study

2018-01-16
----------
- chatted w/ mythmon about how to start up normandy Firefox component
  - will live in toolkit/
  - probably started up in nsBrowserGlue.js for desktop, browser.js for fennec
- worked on enabling system add-on updates on Fennec
    - https://bugzil.la/1260213

2018-01-15
----------
- holiday (MLK)

2018-01-12
----------
- PTO (out sick)

2018-01-11
----------
- worked on enabling system add-on updates on Fennec
    - https://bugzil.la/1260213
- responded to review request about flipping the `app.update.enabled` pref to false when updater is disabled at build time
    - https://bugzil.la/1427471
    - r+'d after a few questions to make sure we wouldn't bust blocklist or SAO updates for desktop or fennec (distro builds do their own thing but I think we'll be OK in this case too)
- responded to feedback request in bug from cliqz about how we're using built-in list of system-addons
    - https://bugzil.la/1426088
- responded to review request about removing all hotfix code from Firefox
    - https://bugzil.la/1356331
    - I think we need to get Fennec to system add-on updates first
        - https://bugzil.la/1260213

2018-01-10
----------
- worked on enabling system add-on updates on Fennec
    - https://bugzil.la/1260213
- advised on tracking protection study

2018-01-09
----------
- start working on enabling system add-on updates on Fennec
    - https://bugzil.la/1260213
- 1:1
- q1 normandy client planning
- spent some time breaking out various update proposals
    - short-term Q1/Q2 move SAO from balrog to normandy
    - medium-to-long-term allow update of omni jar
    - medium-to-long-term move normandy client to Rust

2018-01-08
----------
- went over feedback from faster feature update proposal
- solicted feedback about out-of-process updater concept

2018-01-05
----------
- meeting possibility of using push for triggering updates
- met w/ bdanforth about TP study

2017-11-29
----------
- met w/ bdanforth who is taking over the TP study
- prototyping

2017-11-28
----------
- meetings
- started working on prototype
- pushed old bug w/ cleanup of issues found in AddonsManager found
  with Flow over the finish line
  - https://bugzil.la/1395425

2017-11-21
----------
- wrote firefox-dev post about jsdoc+sphinx integration
  - https://mail.mozilla.org/pipermail/firefox-dev/2017-November/005955.html
- review for high-priority telemetry/addons manager crash
  - aswan is out and kmag is busy
  - https://bugzil.la/1381633
- learned a bit more about constructing proofs using arithmetic circuits
  and multi-party computation, for a prototype
- reviewed one-off experiment
- looked into how to enable legacy add-ons in local beta build
  - `ac_add_options "MOZ_ALLOW_LEGACY_EXTENSIONS=1"`
  - waiting for unbranded builds to be fixed
    - https://bugzil.la/1414450
- coordinated w/ relman about shipping hotfix color distortion in video on AMD
  - https://bugzil.la/1418556

2017-11-20
----------
- landed jsdoc+sphinx+firefox integration \o/
  - https://bugzil.la/1389341
- investigated options for calling standalone rust code
  - Firefox subprocess module can call standalone binaries
    - https://firefox-source-docs.mozilla.org/toolkit/modules/subprocess/toolkit\_modules/subprocess/index.html
  - jsctypes can load a library into an existing process
    - can introduce stability problems and other weird bugs...
  - launching rust when Firefox starts, and IPCing to it
  - launching rust as OS process, and IPCing to it
- investigated using nacl in rust code
  - the crypto lib aka "salt", via the libsodium fork
  - https://cr.yp.to/highspeed/naclcrypto-20090310.pdf
- prepared hotfix for color distortion in video on AMD cards for 57
  - https://bugzil.la/1418556

2017-11-10
----------
- discussed signing options for XPIs
  - in-app vs. profile dir
- read/responded to email

2017-11-09
----------
- met w/ aswan, discussed webextension and shield/system add-ons/etc.
- read/responded to email
- followed up on sandboxing bug that might prevent some system add-ons
  from updating out-of-cycle on 57.0
  - https://bugzil.la/1376814

2017-11-08
----------
- followed up on sandboxing bug that might prevent some system add-ons
  from updating out-of-cycle on 57.0
  - https://bugzil.la/1376814
  - specifically would affect framescripts and contentaccessible chrome/resource
    URLs
  - mythmon is running a test today to see if shield about: page works
    correctly after an update on 57 beta
- discussed tor meeting minutes w/ add-ons folks
  - https://lists.torproject.org/pipermail/tbb-dev/2017-November/000652.html
  - tl;dr - they might not need to be an extension at all; if they do,
    it might not be as complex as it appears (Tor works over HTTPS AFAICT,
    and there are APIs for the proxy stuff).
    - native connect to a standalone app is also doable
    - or, not be an extension at all and spin up a separate firefox process...

2017-11-07
----------
- filed bug to remove client-side Telemetry Experiments support
  - https://bugzil.la/1415284
- reviewed system add-on update to fix search engine geo prefs
  - https://github.com/mozilla/one-off-system-add-ons/pull/71#pullrequestreview-74915429
- discussed w/ shield and AMO folks which suffix to use for shield addon IDs
  - AMO blocks @mozilla.org/com, probably want @\*.mozilla.org/com as well
- 1:1

2017-11-06
----------
- helped francois test system add-on update to roll back TP UI changes, if needed
  - https://gist.github.com/rhelmer/b392e97d0b6ff81c06c205c760050c2b
- discussed removing telemetry experiments w/ add-ons folks
- reviewed system add-on update (TLS middlebox experiment)
  - https://github.com/mozilla/one-off-system-add-ons/pull/70
- worked on tests for tracking protection study
- filed bug about page action icons being too restrictive
  - https://bugzil.la/1414966
  - this would make tracking protection study much easier to do as a webext

2017-11-03
----------
- highlights from the last few weeks:
  - tracking protection study
    - this is on hold til post-57, still working on tests
      - webrequest onBeforeRequest doesn't seem to be firing for the local
        test page
  - trying determine what the post-57 future of bootstrapped add-ons will be
  - thinking about how to make gofaster less of a niche and more of a
    basic part of mozilla
  - soliciting mozillian's opinions on what they'd like to see in etherpad
  - looking at what we can remove post-57 from addons manager
    - old-style hotfix
    - telemetry experiments
    - ???

2017-10-24
----------
- highlights from the last few weeks:
  - only load system add-ons from a built-in list
    - https://bugzil.la/1348981
    - list is generated at build time and packaged into omni jar
    - required some C++ changes, mostly to test properly
- tracking protection study
  - rewrote as legacy-style bootstrapped add-on, using XUL etc
    - not really possible to get the desired UX via webextensions, yet
      - page action restrictions for example (image only, 16x16)
    - blending in with the Firefox UI becomes much simpler
    - it is possible to share enough underlying code with webextension
      impl that there isnt an advantage to having the overhead of communicating
      with an embedded webext
  - started developing this in-tree so mochitest can be used and mozilla
    "try" infra can produce builds
  - probably can't use shield since this needs to run so early in startup
    to be useful... funnelcake will work here and we can test builds from
    the "try" infra (see above)
- reviews on add-ons manager, shield, helped out with various studies
  

2017-08-30
----------
- highlights from the last few weeks:
  - fixed addon manager bug when user has unicode in profile names
    - https://bugzil.la/1389160
    - turns out we don't test this case at all! filed a few test harness
      bugs
      - https://bugzil.la/1392308
      - https://bugzil.la/1395414
  - put up patch to pass Flow null check violations Mossop found
    - https://bugzil.la/1395425
    - nice opportunity to rewrite to async/await to make this sort of bug
      less likely
      - https://reviewboard.mozilla.org/r/174764/diff/1#file5137262
  - worked on tracking protection study
    - https://github.com/rhelmer/tracking-protection-study/
    - refactored existing study to make more configurable at runtime
      - https://github.com/rhelmer/tracking-protection-study/blob/master/extension/Config.jsm
    - used embedded webextension for UI
      - requires message passing to bootstrap.js
      - https://github.com/rhelmer/tracking-protection-study/tree/master/extension/webextension
      - https://developer.mozilla.org/en-US/Add-ons/WebExtensions/Embedded_WebExtensions
    - found some problems with current tracking protection impl for our purposes:
      - onSecurityChange is only sent if the nsIChannel is connected to the document loaded in the currently-focused tab. This means that we can get an accurate count of blocked resources only if the tab is focused - otherwise the onSecurityChange event is only observed once per focus
        - https://bugzil.la/1388916 is filed to fix this
      - lots of known breakage on real-world sites
        - https://bugzilla.mozilla.org/show_bug.cgi?id=1101005
      - API isn't very amenable to adding a WE API, but I think that's the right
        thing to do long-term.
    - resurrected old sphinx-js patches to land in mozilla-central, now that
      Mozilla infra can handle building and hosting sphinx docs
      - https://bugzil.la/1389341

2017-08-01
----------
- bisected regression range for unwanted system add-on first-run behavior
  - https://bugzil.la/1386295
  - was broken by one of the perf improvements in 55
  - causes brand-new system add-ons to not appear on first-run in a new profile

2017-07-31
----------
- meetings at SF office

2017-07-27
----------
- investigated temporary add-on loading issue
  - happens when temp installing an add-on over an existing one, then uninstalling
  - aswan agreed to take a look
  - https://bugzil.la/1359558
- reviews
  - highlight legacy pane when showing details for legacy add-on
    - https://bugzil.la/1372645
  - mentored bug about moving error codes to public AddonManager class
    - https://bugzil.la/553869
    - running into lots of bustage on m-c :/

2017-07-26
----------
- landed work on making shield download+run recipes in early post-startup
  - https://bugzil.la/1383338
  - also uplifted to beta (55)

2017-07-21
----------
- meetings
- worked on making shield download+run recipes in early post-startup
  - https://github.com/mozilla/normandy/pull/895
  - I *think* it's just about done
  - will have to uplift this into the intended release... 55?

2017-07-20
----------
- reviewed + landed patch to hide telemetry experiments from legacy menu in about:addons
  - https://bugzil.la/1371762
- worked on making shield download+run recipes in early post-startup
  - https://github.com/mozilla/normandy/pull/895
  - addressed review feedback

2017-07-18
----------
- investigated spurious system add-on related issue found by QA
  - https://bugzil.la/1382037
- worked on making shield download+run recipes in early post-startup
  - https://github.com/mozilla/normandy/issues/889
- reviews
  - don't show optional legacy pane in about:addons if no disabled legacy add-ons
    - https://bugzil.la/1374637
  - legacy page shows an experiment
    - https://bugzil.la/1371762

2017-07-17
----------
- worked on making shield download+run recipes in early post-startup
  - https://github.com/mozilla/normandy/issues/889
- reviewed pre-publication browser-arch docs

2017-07-06
----------
- Attended browser-arch meeting
- reviewed update-only tls measurement add-on
  - https://github.com/mozilla/one-off-system-add-ons/pull/46

2017-07-05
----------
- started review on moving blocklist into addons DB
  - https://bugzil.la/1377538
  - this should keep the (expensive!) blocklist service from being parsing the whole blocklist at startup
- worked on moving system add-ons to omni jar
  - https://bugzil.la/1357205
  - figuring out exactly where Addon Path Service is used, and if passing omni.ja to it is appropriate...
- looked at addons background update check that fails when new RCWN feature is enabled
  - https://bugzil.la/1358038
  - posted with some thoughts on where the problem might be, needinfo'd network folks offering help making a minimal test case if my suggestions don't pan out

2017-06-21
----------
- took over cache invalidation patch when using embedded webextensions for aswan (pto)
  - https://bugzil.la/1372750

2017-06-15
----------
- filed bug about showing permissions UI on about: pages
  - https://bugzil.la/1373487
- investigated disappearing system add-ons in artifact (dev) build
  - https://bugzil.la/1371273
  - turned out to be profile switching which isn't really well supported :/
    - might disable or strongly encourage profile switching instead...
    - probably will fix it anyway
- participated in browser-arch discussion around multi-process and updates
- worked on bug where system add-on and hotfix updates show up in about:addons
  if it is open during update
  - https://bugzil.la/1367800
  - users still can't disable or remove, so not harmful just looks glitchy
  - again, simple code fix, complex test :/


2017-06-14
----------
- worked on refining updates proposal
- reviewed bug showing unsigned legacy extensions in legacy section
  - https://bugzil.la/1371752
  - this is only for builds that allow disabling signing so pretty minor impact
- worked on bug about race in addons manager module
  - https://bugzil.la/1371363
  - this only happens for firefox-internal callers doing it in the wrong order
    - telemetry was bit by this but fixed it in their code
    - it's a footgun we should remove
  - have it done other than the dang xpcshell test :/


2017-06-09
----------
- reviewed change to always show flash preferences button in about:addons
  - https://bugzil.la/1357300
  - r+'d after a few rounds
- worked on bug involving race condition between uninstall and add-on initialization
  - this is only a problem for internal code using the AddonManager API
  - https://bugzil.la/1371363
- worked on hotfix/system add-ons showing up during update
  - https://bugzil.la/1367800

2017-06-08
----------
- landed string change in time for beta
  - https://bugzil.la/1360777

2017-06-05
----------
- Worked on update proposal
- Resolved bug that was blocking screenshots being enabled by default
  - https://bugzil.la/1355998

2017-05-22
----------
- Responded to QA needinfo on captive portal detection hotfix for 52
  - https://bugzil.la/1365732#c7
- Reviewed test change to enable privileged add-ons
  - Things like Test Pilot will need this post-57 to install
  - https://bugzil.la/1357948

2017-05-16
----------
- too busy to keep on this lately, some highlights from the last few weeks:
  - lots of perf-related addons manager reviews
  - helping to get crash reporting going for extension process
    - https://bugzil.la/1353168
  - Firefox arch review meetings and discussion
  - helped out w/ Screenshots landing
    - also helping to look into perf issues - there are some perf problems
      with using a WebExtension, they may put a bit more of the add-on
      into the bootstrap.js side to mitigate
  - worked on update proposal
  - learning how to better use the gecko profiler

2017-05-08
----------
- finally able to reproduce screenshots bug
  - https://bugzil.la/1355998
  - looks like it only happens on win7 opt, nowhere else
  - also it's in the about:addons windowed code, which is known to
    be buggy and we've announced support to remove anyway \o/
- PTO in afternoon

2017-05-03
----------
- reviewing https://bugzil.la/1356826
    - has a controversial bit that I was holding off on while discussing
- further work to re-enable test that started breaking for screenshots when
  enabled
  - https://bugzil.la/1355998
  - taking lots of time due to waiting for tryserver...
- more investigatory work on moving system add-ons into omni jar
  - https://bugzil.la/1357205
  - this will help startup perf and make malware dropping in a new XPI
    less trivial.
- made suggestions for shipping mortar and pdf.js side-by-side
  - https://bugzil.la/1360494

2017-05-03
----------
- tried to re-enable test that started breaking for screenshots when enabled
  - https://bugzil.la/1355998
  - not able to repro, standard8 thinks it might be due to broken tests
    on m-c, going to try rebasing tmrw,

2017-04-19
----------
- r+ on adding whether add-on is a webextension to telemetry
  - https://bugzil.la/1357460
- looked into why screenshots loaded as temp addon does not seem to
  override the built-in
  - https://github.com/mozilla-services/screenshots/pull/2704
  - turned out this was due to the webextension not being shut down
    by bootstrap shutdown()

2017-04-18
----------
- working on adding whether add-on is a webextension to telemetry
  - https://bugzil.la/1357460
- more reviews


2017-04-17
----------
- so, so many AddonManager perf-related reviews
  - lazy-loading, eliminating directory scanning, etc.
  - ex. https://bugzil.la/1356826
- helped track down screenshots bustage on nightly
  - https://bugzil.la/1357137
  - also chatted w/ screenshots folks about more testing to catch this

2017-04-10
----------
- reviewed and answered addons-related questions for shield-recipe-client
  - https://github.com/mozilla/normandy/pull/670
- closed bug about revealing system add-ons in about:addons
  - reasoning in https://bugzil.la/1231202#c9
- worked on bug to validate built-in system add-ons against list of known IDs
  - https://bugzil.la/1348981
  - this will eliminate one of the dirs we need to scan at startup, which
    we are trying to eliminate from AddonManager for 55.


2017-03-26
----------
- landed unregister for update timer manager
  - https://bugzil.la/1350471
  - this is for shield-recipe-client and other add-ons

2017-03-26
----------
- pushed patch to add unregister method for update timer manager
  - https://bugzil.la/1350471
  - needed because currently there's no way for add-ons to unregister
  - will likely uplift for shield-recipe-client use
    -https://github.com/mozilla/normandy/issues/588

2017-03-24
----------
- doing some self-triage, lots of old bugs hanging around.
- started working on refactoring to reduce the amount of code needed for new install locations in addons manager
  - https://bugzil.la/1314177
  - tl;dr move to ES6 class and use extends, instead of current approach which has a fair amount of duplication.

2017-03-23
----------
- helped w/ review and push of tls-comparison system add-on update
  - https://bugzil.la/1349076
- pushed fix for system add-on update regression in 52
  - https://bugzil.la/1350064
  - tl;dr - updates are not removed on app update
  - took a look at Telemetry and minimal impact, easy to work around but good to be aware of.

2017-03-22
----------
- sent intent-to-remove standalone about:addons UI to dev-platform list
  - https://groups.google.com/forum/#!topic/mozilla.dev.platform/qbIYmhzA_w4
  - https://bugzil.la/1349723

2017-03-15
----------
- pointed felipe at place to add preferences button for Flash in about:addons
- chatted w/ ekr about system add-on experiments
- put up patch to send old version along with upgrade data for temporary add-on reloads
  - https://bugzil.la/1347971
- worked on sphinx+jsdoc integration
  - http://foxdocs.org/toolkit/mozapps/extensions/addon-manager/AddonManager.html

2017-03-15
----------
- PTO

2017-03-14
----------
- PTO

2017-03-03
----------
- pushed PR with proposed fix for tls 1.3 add-on
    - https://github.com/mozilla/one-off-system-add-ons/pull/20
    - listens for "loadend"
    - also sets deadman timer per ekr's suggestion
- reviews
- r+ on system add-on update test which is timing out in moz infra

2017-03-02
----------
- looked into tls 1.3 data w/ ekr and felipe
    - small percentage of users keeping 1.3 on longer than expected
    - was able to reproduce using theory from felipe - "load" listeners are not called on timeout but they are on "loadend".
        - used xcode "link conditioner" to simulate super lossy connection
    - ckprice setting up post-mortem
- reviews

2017-03-01
----------
- converted tls1.3 telemetry experiment to system add-on
    - https://github.com/mozilla/one-off-system-add-ons/commit/928d617ab8a5cf10158717bcde7168ace10df35a
- wrote better docs on system add-ons, waiting for gecko.rtd push
- investigated building+hosting jsdocs somewhere (probably GH pages, RTD can't do it :/)

2017-02-25
----------
- helped QA test restartless system addon patch on beta (52)
    - https://bugzil.la/1204156
- looked at SHA1 deprecation issue QA was seeing
        - got them to send profile, couldn't repro
    - turns out to be using unexpected builds

2017-02-24
----------
- worked w/ Telemetry team to vet (and correct) system add-on uptake graphs

2017-02-21
----------
- reviews
- PageShot meeting
- discussed toolkit/browser split for discopane
    - update messages must be loaded into browser

2017-02-16
----------
- reviews
- discussed PageShot shipping options w/ ianbicking
- discussed Active Stream shipping on fx-dev list
- investigated omni-jar improvements
    - looks doable to move system add-ons into here
    - should yield startup time improvement + partial patch reduction

2017-02-15
----------
- refining telemetry dashboards to track system add-on rollout
  - https://sql.telemetry.mozilla.org/queries/2654#4910
  - https://sql.telemetry.mozilla.org/queries/2683#4994
    - looking into refining query
      - excluding clients that have not reported since the update was made available.
- tested various omni.ja compression improvements
    - https://bugzil.la/1231379
    - catlee re-opening bug to ship uncompressed omni.ja, which:
        - reduces partial diff size (Windows, Release) by ~40%
        - improves startup time by ~2-3%
    - known downsides are
        - seems to cost about ~8 MB RAM
- investigated other omni.ja improvements

2017-02-06
----------
- working on telemetry dashboards to track system add-on rollout
  - https://sql.telemetry.mozilla.org/queries/2654#4910
  - https://sql.telemetry.mozilla.org/queries/2683#4994
    - looking into refining query
      - excluding clients that have not reported since the update was made available.

2017-02-03
----------
- working on telemetry dashboard to track system add-on rollout
  - https://sql.telemetry.mozilla.org/queries/2654/source#4910
- responded to review request on webextensions-themes add-on manager integration
  - https://bugzil.la/1330349

2017-02-02
----------
- looked into telemetry for low uptake of hotfix
  - working on telemetry dashboard to track hotfix uptake
    - https://sql.telemetry.mozilla.org/queries/2634/source#4903

2017-02-01
----------
- shipped system add-on diagnostics update
  - https://bugzil.la/1307568
  - working on telemetry dashboard to track system add-on rollout
    - https://sql.telemetry.mozilla.org/queries/2654/source#4910

2017-01-31
----------
- worked on system add-on diagnostics update
  - https://bugzil.la/1307568
  - for the update-only, re-submitted fixed version for signing+QA

2017-01-30
----------
- worked on system add-on diagnostics add-on
  - https://bugzil.la/1307568
  - built-in version got almost-final-r+
  - update-only version, QA tested and found an issue
- reviewed data from telemetry/metrics regarding hotfix uptake
  - 10% of main summary (instead of longitudinal) shows 90% uptake
    - longitudinal only showed ~55% shortly after release, up to ~77%...

2017-01-25
----------
- chatted w/ devtools
- quick chat about graduating add-on to built-in
- put doc up for data review for diagnostic system add-on
    - https://bugzil.la/1307568

2017-01-24
----------
- worked on diagnostic system add-on
    - https://bugzil.la/1307568
    - general approach is:
        - measure first
        - ship simple update-only version ASAP
            - sent "intent to ship" email to r-d and gofaster lists
        - land more complete version in the tree
- quick followup review on "your add-on is ready" pop-up
    - https://bugzil.la/1308310

2017-01-23
----------
- caught up on review and feedback requests
  - post-install notification for mozAddonManager installs
    - https://bugzil.la/1308310
  - "use strict" violations only logged at LOG level
    - https://bugzil.la/1096135
- started working on breaking up test that intermittently times out
  - https://bugzil.la/1324192

2017-01-18
----------
- chatted w/ felipe about diagnostic add-on
  - https://bugzil.la/1307568
  - plan is to
    1. ship as an update and track uptake
    2. ship built-in and look at diagnostic telemetry
    3. re-ship update once restartless system add-ons go out in 52

2017-01-17
----------
- caught up on reviews and feedback requests

2017-01-09 -> 2017-01-13
------------------------
- mostly out due to storm knocking out internet connection
- responded to review/feedback requests

2017-01-05
----------
- reviewed the first half of webext permission prompt patches
  - https://bugzil.la/1308295
- chatted w/ devtools team about upcoming plans
- fixed even more test failures for ServiceRequest (TLS 1.3 disabling XHR replacement) onto beta
  - https://bugzil.la/1325501
  - mostly just minor stuff like imports that haven't made it to beta yet
  - looks like it stuck this time \o/
- re-ran try for browser.runtime.oninstalled temporary add-on fix
  - https://bugzil.la/1323938
  - should be ready, but hopefully try is less busted now
- investigated using re:dash for tracking distribution of system add-on versions
  - https://bugzil.la/1323547


2017-01-04
----------
- investigated using re:dash for crashes involving specific add-ons
- fixed test failures for ServiceRequest (TLS 1.3 disabling XHR replacement) onto beta
  - https://bugzil.la/1325501
- reviewed shield addon change (startup pref check shouldn't throw first time)
  - https://bugzil.la/1325797
- vouched for level 3 access for mythmon
  - https://bugzil.la/1328433

2017-01-03
----------
- catching up from PTO
- rebased ServiceRequest (TLS 1.3 disabling XHR replacement) onto beta
  - https://bugzil.la/1325501
  - s/rebased/rewrote/ is more like it :/
- feedback on aswan removing support for multiple installs via InstallTrigger
  - https://bugzil.la/1323129
- feedback on markh's work on getting sync to reliably tell which addons
  came from AMO and are therefore eligible for syncing
  - https://bugzil.la/1285866
  - tl;dr - we should keep the list of add-ons installed from AMO more
    consistent, AFAICT we only populate this "DB" (really a JSON file)
    once per day along with the addons check.
- 1:1
- skipped out on addons manager triage due to plumbing-related issues :O

2016-12-20
----------
- swapped PTO day to look into conservative TLS settings bug
  - https://bugzil.la/1323538
  - tl;dr - bleeding edge features like TLS 1.3 are breaking some updates
  - instead of playing whack-a-mole patching every place in Firefox chrome code
    that does XHR, consulted w/ ehsan about doing it in the XHR implementations
    instead. put up patch with f?ehsan
- finished review for shield system add-on
  - https://bugzil.la/1308656
  - was landed this evening \o/

2016-12-16
----------
- AddonManager triage
- reviewed patch to promisify AddonManager
  - https://bugzil.la/987512
  - can optionally handle callbacks which is cool

2016-12-15
----------
- one-off gofaster meeting to talk about uptake investigation
  - pretty sure we're having the same problem as GMP and Hotfix have before
  - diagnostic addon and better telemetry dashboard should give a starting point

2016-12-14
----------
- worked on new diagnostic system add-on to ship with Firefox to determine
  why all System Add-on (incl. GMP) updates are not making it to all
  users
  - https://bugzil.la/1307568
- filed bugs
  - track uptake of all Firefox updates
    - https://bugzil.la/1323547
    - followup from meeting during workweek
  - use conservative TLS settings for add-on updates
    - https://bugzil.la/1323538
    - related to recent concerns about App Update over TLS 1.3
  - followup about rebuilding missing or corrupt Addon DB (JSON)
    - https://bugzil/la/1323594
- reviews
  - finished with patch removing support for multipackage XPIs
    - https://bugzil.a/1323128
  - started on patch to remove support for multiple XPIs with one InstallTrigger
    - https://bugzil.la/1323129
- needinfo
  - started looking at restored session sync bug
    - https://bugzil.la/1321119

2016-12-13
----------
- PTO

2016-12-12
----------
- PTO for most of the day
- set up a test scenario for QA and restartless system add-ons
  - https://bugzil.la/1204156#c55

2016-11-29
----------
- minor fallout for uplift request for e10srollout-supporting change
  - https://bugzil.la/1272446
  - I had forgotten to `hg add` the unit test on the beta branch,
    so it didn't appear in the diff /o\
    - also, was wrong that Aurora didn't need its own patch
  - attached new patches for beta and aurora which stuck \o/
- did some addons manager triage of existing open bugs w/ aswan
- responded to webextensions concerns on dev-addons list
- blogged about a few side projects
  - http://rhelmer.org/blog/aboutaddons-in-react.html
  - http://rhelmer.org/blog/toy-add-on-manager-in-rust

2016-11-28
----------
- uplift request for e10srollout-supporting change
  - https://bugzil.la/1272446
- reviews
  - remove string generics
    - https://bugzil.la/1319939
  - e10srollout target all addons not explicitly marked non-multiprocess-compatible
    - https://bugzil.la/1314429
- checked in with Gijs and mythmon regarding SHIELD client
  - mythmon is porting over tests and removing SDK, all systems go
    - https://bugzil.la/1308656

2016-11-23
----------
- helped out w/ getting shield recipe client system add-on build+test in moz-central working
  - https://github.com/mythmon/normandy-addon/pull/1
  - https://github.com/mythmon/normandy-addon/pull/2

- GoFaster meeting
- Felipe ran into an issue with AddonManager and e10srollout where he wants to identify
  whether add-ons explicitly opted out of multiprocess compatibility, but currently
  only a boolean is stored after the manifest is parsed.

  Worked on providing a way to cause all manifests to be re-read when the addons DB
  schema version is bumped - this way Felipe could add a new property to the DB which is
  set based on the presence of the multiProcessCompatible property, and all add-on
  manifests will be re-read when a schema version bump comes with the next app update.

  - https://bugzil.la/1272446


2016-11-21
----------
- started chatting w/ folks about felipe's idea for update experiment
  - https://bugzil.la/1307568
  - tl;dr we suspect MITM proxies are breaking different updates, including
    but not limites to system add-ons, due to cert pinning requirements
- looked into what happens when balrog sends 404 to GMP/SystemAddon update
  - currently HTTP status is ignored :/ so XML is read, but will throw if
    can't be parsed
    - TODO file bug
- responded to some needinfos
  - Firefox for Android sending bad versions in GMP updates
    - https://bugzil.la/1319200
  - Addons manager does not store difference between unset multiprocess and
    set xplicitly false in manifest
    - https://bugzil.la/1314429
    - we should be able to do this by bumping the schema version and adding
      a new property to store this. the schema bump should cause all addon
      manifests to be re-read.

2016-11-11
----------
- landed restartless system add-on patch \o/
  - https://bugzil.la/1204156

2016-11-14
----------
- reviewed AddonInstall refactoring patch
- worked on refactoring all of AddonManager to es6 classes
  - want to increase use of subclasses and tighten design, this is first part

2016-11-14
----------
- worked on issue with sync addon DB loading throwing exception when
  dev edition theme is the default
  - https://bugzil.la/1313960
  - the issue of why we are doing sync load here is a tricky one... for now
    going to settle for making the exception go away (seems to just be a case
    of a programmer error+no test around interrupting async load when sync
    load has completed in the meantime.

    Going to split out the "how to make this right" issue from the "make
    it work as intended"

2016-11-03
----------
- addressed review comments on restartless system addon patch
  - https://bugzil.la/1204156

2016-11-02
----------
- chatted w/ rdalal on what needs doing in morgoth
  - https://github.com/mozilla/morgoth/issues/46
- AddonManager triage w/ aswan
- filed bug to remove install.rdf and replace w/ manifest.json
  - basically make all bootstrap.js addons "hybrid" type
  - https://bugzil.la/1314710
- got Rust compiling to wasm working locally
  - maybe can use for Firefox eventually
    - better type safety/correctness than JS
    - no GC w/ memory correctness
    - no parallelism yet, but SharedArrayBuffer coming

2016-10-31
----------
- took a look at error message from theme selector
  - https://bugzil.la/1313960
- caught up on email/bugmail

2016-10-19
----------
- met w/ rdalal about https://github.com/mozilla/morgoth/issues/41
- reviews
  - mozAddonManager should use frame manager, to work w/ e10s
    - https://bugzil.la/1311180
  - fix for unsafe CPOW warnings in xpinstall tests
    - https://bugzil.la/1311459

2016-10-14
----------
- starting working on https://github.com/mozilla/morgoth/issues/41
  - read through morgoth data model
- reviewed bug regarding bad interaction between Addon SDK and e10srollout
  - https://bugzil.la/1304392

2016-10-13
----------
- reviewed bug: install addons permanently using proxy file from about:debugging
  - https://bugzil.la/1309288

2016-10-12
----------
- morgoth working locally
  - https://github.com/mozilla/morgoth/pull/47
- worked more on restartless system addon install+update
  - patch working locally
  - going through test failures

2016-10-11
----------
- so many meetings
- started working on morgoth
- worked on separating system add-on components in about:support
  - https://bugzil.la/1308981

2016-09-29
----------
- landed patch for about:crashes to separate un/submitted entries
  - https://bugzil.la/512479
- started watching the "ES6 For Everyone" training videos
  - a kind mozillian gifted me a pass
- fixed bug in onUpdateAvailable that was causing test failures
  - https://bugzil.la/1306492

2016-09-28
----------
- revived patch for about:crashes to separate un/submitted entries
  - https://bugzil.la/512479
  - had more tests already than I realized, mostly working through those

2016-09-27
----------
- meetings
  - gofaster
  - system addons
  - addonmanager triage

2016-09-17
----------
- landed webcompat system add-on consistency
  - https://bugzil.la/1303514
- restartless install+update for system add-ons
  - https://bugzil.la/1204156
  - chatted w/ aswan, going to need to move the postponed AddonInstall state

2016-09-16
----------
- so many meetings
- made webcompat system add-ons more consistent
  - https://bugzil.la/1303514

2016-09-05 -> 2016-09-09
------------------------
- In Portland office for meetings
  - figured out plan for automating system add-on update signing
  - helped w/ crash collector transition planning
- restartless install+update for system add-ons
  - https://bugzil.la/1204156
  - working patch locally, needs more testing

2016-09-01
----------
- looked at patch backed out of autoland
  - https://bugzil.la/557710
  - the test code I refactored is used in more places than I realized
    - going to refactor this and all callers first
      - https://bugzil.la/1298467

2016-08-26
----------
- put up patch for review on prereq to install+update for system add-ons
  - https://bugzil.la/557710
  - filed a few followup bugs
    - improve testing functions for programmatically creating addons
      - https://bugzil.la/1298467
    - temporary add-ons do not reveal overridden add-ons in the correct order
      - https://bugzil.la/1298545

2016-08-25
----------
- helped merge updates-only system add-ons patch to aurora+beta
  - https://bugzil.la/1295732
- worked on prereq to restartless install+update for system add-ons
  - https://bugzil.la/557710

2016-08-24
----------
- started working again on restartless install+update for system add-ons
  - https://bugzil.la/1204156
  - posted plan to bug

2016-08-23
----------
- addons triage
- picked up bug about distribution add-ons not working on Fennec
  - https://bugzil.la/1296563
  - turns out was a documentation bug
- reviewed bug to expose canUninstall flag for AOM-exposed content
  - https://bugzil.la/1297028

2016-08-19
----------
- landed feature to leave built-in system add-ons alone, only specify updates
  - https://bugzil.la/1295732
  - requested uplift to aurora+beta

2016-08-15
----------
- landed delayed update for webextensions
  - https://bugzil.la/1279012
- working on prereq to system add-on changes
  - https://bugzil.la/557710
- reviewed moving AddonManager test helpers to shared module
  - this is so it can be easily used by webextensions too
  - https://bugzil.la/1294811

2016-08-12
----------
- r+ on delayed update for webextensions \o/
  - https://bugzil.la/1279012
  - can't land yet, seems to be some mozreview bug :/
- started working on prereq to system add-on changes
  - https://bugzil.la/557710

2016-08-11
----------
- PTO

2016-08-10
----------
- helped with system add-on roll-out
  - Pocket had some l10n issues
    - xpi shipped w/ Firefox only has en-US, need one with all locales
- fixed bugs from try run on onUpdateAvailable
  - https://bugzil.la/1279012
  - re-ran try build
- took older bug to add better tests for same add-onmultiple install locations
  - https://bugzil.la/557710
  - need this for avoiding re-downloading (and signing+hosting) for default
    system add-ons
    - https://bugzil.la/1273709

2016-08-09
----------
- addressed review feedback for onUpdateAvailable
  - https://bugzil.la/1279012
  - added better test for browser.runtime.reload()
  - re-ran try build

2016-08-08
----------
- helped out with "out of date notification" system add-on
  - https://bugzil.la/1292562
- addressed review feedback for onUpdateAvailable
  - https://bugzil.la/1279012
  - added better test for browser.runtime.reload()
  - re-ran try build

2016-08-05
----------
- looked into issues testing system add-on for Firefox 44 on Windows XP
  - https://bugzil.la/
  - turned out AMO was serving a bad update, now fixed
    - https://github.com/mozilla/addons-server/issues/3228
- almost done addressing review feedback for browser.runtime.onUpdateAvailable
  - https://bugzil.la/1279012
  - should add better test for browser.runtime.reload() too

2016-08-04
----------
- in SF office, meetings etc.
- check if bad manifest (loaded from XPI) is cached
    - e.g. "strict version" is set then later removed
- worked on monotonically-increasing revision for system add-ons
  - https://bugzil.la/1292031
  - have a patch, needs tests
    - https://gist.github.com/Osmose/88eb585a302299394a076df11be52fd5

2016-08-03
----------
- Existing JS scoping bug was fixed, which caused a system add-on test to fail
  - https://bugzil.la/1291569
  - turns out it wasn't running the tests we thought it was, fortunately only
    one minor feature had a legit broken test (empty add-on set means to remove
    all updates and to disable all built-in add-ons) - will probably just remove
    the feature.
      - https://bugzil.la/1287191
- Added a few bugs to Osmose's system add-on revision tracking bug
  - Ensure that all default system add-ons are present in Balrog response
    - https://bugzil.la/1292029
  - Use monotonically-increasing revision number from Balrog for each update set
    - https://bugzil.la/1292031

2016-08-02
----------
- worked on postponed support for webextensions
  - https://bugil.la/1279012
  - pushed patch for review
- worked on making WebExtension tests better
  - https://bugzil.la/1290617
  - merged to inbound (needed for https://bugzil.la/1279012)

2016-07-29
----------
- worked on postponed support for webextensions
  - https://bugil.la/1279012
  - basically done, making tests nicer
    - things like message passing from AddonManager -> WebExtension are hard
    - lots of divergence across AddonManager/WebExt tests
- worked on making WebExtension tests better
  - https://bugzil.la/1290617
  - patch is pushed, waiting for review

2016-07-26
----------
- looked into QA results for "delayed add-on" patch
  - https://bugzil.la/1231172#c73
- worked on postponed support for webextensions
  - https://bugil.la/1279012
- added file extension feature to web-ext
  - https://github.com/mozilla/web-ext/pull/392
  - this is making it painful to work on postponed support for webextensions

2016-07-25
----------
- meeting w/ mixedpuppy about gofaster
- worked on postponed support for webextensions
  - https://bugil.la/1279012

2016-07-22
----------
- review
- made sure we can re-enable disabled hidden/system add-ons via update
  - they can no longer be disabled as of https://bugzil.la/1281077
    but wanted to ensure that they will be re-enabled
  - was working on https://bugzil.la/1283963 but maybe not needed?

2016-07-21
----------
- worked on ensuring system add-ons are enabled during updates
  - https://bugzil.la/1279012
- worked on postponed upgrade support for system add-ons
  - https://bugzil.la/1204156

2016-07-20
----------
- review for lock down on mozAddonManager.install()
  - https://bugzil.la/1287125
- worked on ensuring system add-ons are enabled during updates
  - https://bugzil.la/1279012
- PTO in the afternoon

2016-07-19
----------
- helped flesh out dynamic theming API for web extensions
  - https://github.com/nt1m/WebExtensions-Theming-API/blob/master/Proposal.md
- worked on allowing system add-ons to upgrade w/o restart
  - https://bugzil.la/303368

2016-07-18
----------
- reviewed bug to treat corrupt addons.json in AddonRepo as if it were missing
  - https://bugzil.la/1286785
- drafted+sent email about DETH proto progress
- chatted w/ ddurst+willkg about what it'd take to fix snappy
- follow up on backout on patch landed for aswan
  - https://bugzil.la/1287125
  - he is back and can finish investigating
- chatted about symbolapi woes with various folks
- chatted about webextensions dynamic theming in #webextensions
  - https://github.com/nt1m/WebExtensions-Theming-API/blob/master/Proposal.md#dynamic-theming-theming-elements-globally

2016-07-14
----------
- reviewed patch to further lock down navigator.mozAddonManager
  - https://bugzil.la/1287125
- responded to standard8's gofaster email with more details about process
  changes/improvements in-progress

2016-07-13
----------
- chatted w/ Osmose about r-
  - just mozreview misunderstanding
  - https://bugzil.la/1284564
- chatted w/ markh about "only sync AMO hosted add-ons" woes
  - https://bugzil.la/1285866
  - going to do something like `addon.isHosted` in AddonManager API probably
    - https://bugzil.la/1285866#c3

2016-07-12
----------
- did a little symbolapi investigation
  - looking at strace output w/ ddurst, race condition with files seems possible
  - concurrency model is a bit baffling - there's tornado and concurrent.futures in use, and there are two processes. Need to figure this out before we can determine the problem for sure and make appropriate fix.
- PTO in the afternoon

2016-07-11
----------
- reviewed add-on manager sync bug
  - https://bugzil.la/1275139
- responded to needinfo (testing needed) on new balrog throttle feature
  - https://bugzil.la/1281347
- looked at snappy service strace output we added to watchdog script last week
  - looks like it is stuck trying to read past the end of a cache file...
- started fleshing out DETH prototype
  - https://github.com/rhelmer/deth-proto
  - basic GET, DELETE, POST now work with local zone file

2016-07-06
----------
- early morning telemetry meeting
- starting reviewing patch to avoid syncing hidden/system add-ons
  - https://bugzil.la/1275139
  - chatted w/ markh about this in London, plan is to only sync add-ons
    in the profile, and have an isSyncable getter in the AddonManager API for
    Sync to use.

2016-07-05
----------
- filed bug with doc fix for system add-on spec
  - https://bugzil.la/1284564
  - also tested this and noticed a potential bug in the "default" case, may
    need a followup - see https://bugzil.la/1284564#c2

2016-07-01
----------
- investigated and added patch for reloading temporary web extensions
  - https://bugzil.la/1283897
- worked on allowing system add-ons to delay upgrade
  - https://bugzil.la/1204156

2016-06-30
----------
- landed bug preventing users from disabling hidden/system add-ons
  - https://bugzil.la/1281077
- worked on allowing system add-ons to delay upgrade
  - https://bugzil.la/1204156
  - this requires making them install more like normal add-ons, and
    removing a lot of the current hard-coding.
  - mostly working now, getting tests to pass and need to make some
    decisions like what to do if a set fails to upgrade. Also, one
    add-on delaying needs to delay upgrade for the whole set...
- looked into about:debugging temporary add-on loader issue w/ billm and kmag
  - https://bugzil.la/1283676
  - this is really a platform bug in nsIFilePicker, filed a bug to look into
    that
    - https://bugzil.la/1283680
      - looks dead easy on Mac: https://developer.apple.com/library/mac/documentation/Cocoa/Reference/ApplicationKit/Classes/NSOpenPanel\_Class/index.html
      - Windows (Vista+) and GTK would need more work, might be more than this feature warrants :/
      - given that, might make sense to have a better workaround in the UI

2016-06-29
----------
- worked on bug preventing users from disabling hidden/system add-ons
  - https://bugzil.la/1281077

2016-06-28
----------
- PTO

2016-06-27
----------
- pushed willkg's patch for snappy symbolication server
  - https://github.com/mozilla/Snappy-Symbolication-Server/issues/25

2016-06-23 -> 2016-06-24
------------------------
- mostly out sick
- a few small reviews

2016-06-22
----------
- Helped out w/ Brotli system add-on hotfix
  - https://bugzil.la/1273547
  - lack of XPI provider debugging made this harder than it should be
    - filed https://bugzil.la/1281547 and pushed patch for review

2016-06-21
----------
- about:performance allows disabling system add-ons
  - attached patch to https://bugzil.la/1260450, needs tests
  - AddonManager should just ignore userDisabled state too, for system addons
    - https://bugzil.la/1281077
- 1:1

2016-06-19
----------
- chatted w/ add-on author nt1m about extending an API to control themes,
  so extensions can do dynamic theming in a way that will work for themes
  like CTR, VivaldiFox, Colorful Tabs, etc.

  - https://github.com/nt1m/WebExtensions-Theming-API/blob/master/Proposal.md
  - https://github.com/nt1m/vivaldi-fox/issues/24

2016-06-13 -> 2016-06-17
------------------------
- Mozlondon

2016-04-28
----------
- pushed review for stub for webcompat fix system add-on
  - https://bugzil.la/1268197
  - landed
- pushed request for feedback for delaying add-on upgrade patch
  - https://bugzil.la/1231172
- reviewed stackwalker changes to expose symbol URLs
  - https://github.com/mozilla/socorro/pull/3306
- reviewed adding telemetry count for addon compat dialog
  - https://bugzil.la/1268548

2016-04-19
----------
- looking into converting hello and pocket to web extensions

2016-04-18
----------
- reviews
  - filling in for mossop
- in MV for the day

2016-04-07
----------
- reviews
  - finished review for bug exposing addons to web content
    - https://bugzil.la/1245571

2016-04-05
----------
- meetings
  - chatted w/ luke about tracking protection
  - chatted with bbell about UX for tracking protection addon
  - Go Faster meeting
  - 1:1
- pushed latest UX changes for stop-tracking addon

2016-04-04
----------
- review bug exposing addons to web content (for AMO only)
  - https://bugzil.la/1245571
- worked on providing AddonManager API to support delaying restartless updates
  - https://bugzil.la/1231172

2016-03-10
----------
- looked into Socorro issue since everbody else is out today
  - https://bugzil.la/1255444
- worked on tracking protection add-on
  - https://github.com/rhelmer/stop-tracking
  - quick informal UX review from bwinton

2016-02-05
----------
- finished reviews
  - https://bugzil.la/1246151
    - fixed heroku token so auto-land works for symbols.m.o again
  - https://bugzil.la/1244357
  - https://bugzil.la/1244302
- r+ on telemetry environment bug
  - https://bugzil.la/1232222
  - addressed final review suggestions
  - added "checkin-needed" keyword, as autoland is disabled at the moment

2016-02-04
----------
- PTO

2016-02-03
----------
- put telemetry environment patch up for review
  - now blocking pocket/hello, needs uplift
  - https://bugzil.la/1232222
- reviews
  - https://bugzil.la/1244357

2016-02-02
----------
- continued working on telemetry environment patch up for review
  - need to inject system add-on before startup
  - https://bugzil.la/1232222
- reviews
  - https://bugzil.la/1244357

2016-02-01
----------
- starting reviewing cert DB shim
  - https://bugzil.la/1244357
- worked on adding test to telemetry side of https://bugzil.la/1232222
- gave some guidance in symbolapi outage bug
  - https://bugzil.la/1244589
  - vladan was managing this and has left
  - shout-out to my rust replacement
    - https://github.com/rhelmer/symbolapi
    - works on heroku!

2016-01-29
----------
- reviews
- worked on adding test to telemetry side of https://bugzil.la/1232222
- meeting

2016-01-28
----------
PTO

2016-01-27
----------
- worked on adding test to telemetry side of https://bugzil.la/1232222
  - the way telemetry tests add-ons makes this a little more difficult
    than what we do for add-ons manager, as there's no simple way to
    restart the AddonManager and the system add-on must be present in
    the features dir when the add-ons manager starts up

2016-01-26
----------
- 1:1
- addressed review comments on bug adding system add-on status to telemetry
  - https://bugzil.la/1232222
- reviewed sideloading bug
  - https://bugzil.la/1237820
- learned more about service workers
  - https://serviceworke.rs
- researched Electron (the shell Atom and Brave use)
  - uses node.js and brightray (not CEF)
    - "thin shim over Chromium's Content module"
    - https://github.com/atom/brightray
  - not if it has process separation, or at least chrome/content distinction
    - looks like the chromium content module embedding supports sandboxing
      - http://www.chromium.org/developers/content-module

2016-01-25
----------
- Put up review for adding system add-on status to telemetry environment
  - https://bugzil.la/1232222
  - addressed first round of review comments
- reviewed bug tracking whether a user has been offered side-loaded add-on
  - https://bugzil.la/1237820
- informal code review for mythmon

2016-01-22
----------
- PTO

2016-01-21
----------
- PTO except for:
  - early-morning Balrog+Hello meeting
    - https://public.etherpad-mozilla.org/p/gofaster-balrog
  - took misbehaving laptop to SF office
  - Rust meetup in SF office
2016-01-20
----------
- landed Object.values() removal, asked for approval to uplift to aurora
  - https://bugzil.la/1239484
- worked on providing AddonManager API to support delaying restartless updates
  - https://bugzil.la/1231172
- took a look at https://github.com/brave/browser-laptop
  - `LICENSE.txt` says MPL, uses http://electron.atom.io/

2016-01-19
----------
- Object.values() isn't riding the trains, put up a review request to modify
  some ESLint-related refactoring
  - https://bugzil.la/1239484
- worked on providing AddonManager API to support delaying restartless updates
  - https://bugzil.la/1231172
- gofaster meeting

2016-01-13
----------
- worked on providing AddonManager API to support delaying restartless updates
  - https://bugzil.la/1231172
- portland meetings

2016-01-13
----------
- flew to portland for meetings
- worked on providing AddonManager API to support delaying restartless updates
  - https://bugzil.la/1231172

2016-01-12
----------
- worked on providing AddonManager API to support delaying restartless updates
  - https://bugzil.la/1231172
- prep for portland trip

2016-01-11
----------
- worked on providing AddonManager API to support delaying restartless updates
  - https://bugzil.la/1231172
  - web extensions need this too, e.g. https://bugzil.la/1213473
- responded to question about real-time telemetry for system add-ons
  - https://bugzil.la/1232569

2016-01-08
----------
- PTO

2016-01-07
----------
- Meetings in SF

2016-01-06
----------
- made some progress on https://bugzil.la/1232222 and https://bugzil.la/1230688

2016-01-05
----------
- Go Faster meeting
- Landed Bug 1209344 - Link to about:debugging from about:addons

2015-12-07 -> 2015-12-11
------------------------
- Mozlando

2015-11-24
----------
- reviewed a bunch of patches
    - https://bugzil.la/1226386
- gofaster meeting

2015-11-23
----------
- restartless add-on patch merged to fx-team
    - https://bugzil.la/1209341
- worked on Hello-as-addon blockers

2015-11-18
----------
- r+ on restartless add-on patch \o/
    - https://bugzil.la/1209341
- reviewed signature verification for hotfixes
    - https://bugzil.la/1225629
- reviewed removal special casing of experiments
    - https://bugzil.la/1220911
- working with Hello team on landing Hello-as-addon

2015-11-04
----------
- discussed Socorro Fennec problem w/ peterbe
    - reviewed+merged peterbe's fix https://bugzil.la/1221624
- all but one review comments done on unsigned restartless add-on patch
    - https://bugzil.la/1209341
- started addressing review comments from Standard8 on Hello-as-addon
    - https://github.com/mozilla/system-addons/tree/bug1186172-loop-as-addon
    - a few more to go...

2015-11-03
----------
- work through review comments on unsigned restartless add-on patch
    - https://bugzil.la/1209341
- met w/ phrawzty
- met w/ Hello team about landing add-on
    - discussed what it would take to land, planned a few followups:
    - pinged glandium about moz-central add-on packaging
        - https://bugzil.la/1216371
    - worked on rebasing system-addons repo against master
        - https://github.com/mozilla/system-addons/tree/bug1186172-loop-as-addon

2015-11-02
----------
- chatted w/ mixedpuppy regarding pocket-as-addon
    - https://bugzil.la/1215694
- put up "loading unsigned restartless add-ons at runtime" patch for review
    - https://bugzil.la/1209341
    - a few FIXME/TODOs in there, expect to have to resolve before landing

2015-10-19
----------
- worked on skinning problem with loop add-on
    - toolbar icon is 36px but needs to be resized to 24px
        - now a user stylesheet, used to be done in browser.css somewhere
    - finally figured this out, thanks to gijs and dolske in #fx-team

2015-10-16
----------
- more work on loading unsigned restartless add-ons at runtime
    - https://bugzil.la/1209341

2015-10-15
----------
- more work on loading unsigned restartless add-ons at runtime
    - https://bugzil.la/1209341
    - tests work OK but not working from actual runtime yet

2015-10-14
----------
- more work on loading unsigned restartless add-ons at runtime
    - https://bugzil.la/1209341
    - made substantial progress - working through some test failures
- PTO in the afternoon

2015-10-13
----------
- worked on loading unsigned restartless add-ons at runtime
    - https://bugzil.la/1209341
- PTO in the afternoon

2015-10-12
----------
- pushed latest loop-as-addon changes to system-addons fork
    - https://github.com/mozilla/system-addons/pull/6
    - only outstanding issue is toolbar icon size
        - mbanner is going to help take a look
- worked on loading unsigned restartless add-ons at runtime
    - https://bugzil.la/1209341
- took a look at current Places UI
    - chrome uses (much simpler) separate UIs for bookmarks, history, etc.
        - implemented in HTML

2015-10-09
----------
- figured out Socorro permissions problem
    - crashmover was not running as proper user, if it ran first it'd
      create a directory that socorro user could not write to
- PTO afternoon (out sick)

2015-10-08
----------
- met w/ mossop regarding system-addon build+deploy pipeline
    - notes: http://etherpad.io/p/system-addons-build-deploy
- looked at Socorro collector permissions problem a bit more
    - just started happening on staging, jp to file bug if it keeps happening
    - probably a bug in RPM packaging
- made progress on porting over loop skin
    - wrestling with CSS - used CPP #include in ./browser :/

2015-10-07
----------
- helped look at Socorro collector permissions problem
- discussed build/release strategy for system-addons
    - planning on installing system add-on unpacked in appdir
    - shipping xpi in final build for startup/runtime perf
    - this seems to work already \o/

2015-10-06
----------
- Go Faster meeting
- finished reviewing "purge outdated system add-ons" bug
    - https://bugzil.la/1192928
- rebased system-addons fork, tested loop
    - works but requires signing currently

2015-10-05
----------
- met w/ dmose in SF about Hello
- TAG meeting
- reviewed bug for purging outdated system add-ons
    - https://bugzil.la/1192928

2015-10-02
----------
- discussed config/secrets mgmt w/ peterbe for socorro
    - https://bugzil.la/1210888
- tryserver run for jgriffin to review
    - https://treeherder.mozilla.org/#/jobs?repo=try&revision=57d024388131
- started working on loading unsigned restartless add-ons at runtime
    - https://bugzil.la/1209341
- let devtools folks know about "system add-ons" plans
    - https://bugzil.la/1203159#c8

2015-10-01
----------
- met with jgriffin/catlee/jp about build + test
    - https://docs.google.com/document/d/13QdD5LQWvjoP1HbMI605HZFW8xhthwnzBPgVJueNJ_0
- reviewed https://bugzil.la/1193973
- rebased loop add-on prototype for mbanner to review
    - put on gh to make it easier
        - https://github.com/mozilla/system-addons/pull/6

2015-09-30
----------
- met with mbanner re: loop-as-addon
    - https://docs.google.com/document/d/107M5HH9bb7ARfbh2uVVeMoMe2__dM7mXMIsQAGsOnq0/
- investigated allowing unsigned restartless add-ons for dev purposes
    - https://bugzil.la/1209341

2015-09-29
----------
- Go Faster meeting
- PTO in the afternoon
- finished reviewing remaining system-addons bugs
    - https://bugzil.la/1193973
    - https://bugzil.la/1204159
    - https://bugzil.la/1207772

2015-09-28
----------
- reviewed remaining system-addons bugs
    - https://bugzil.la/1193973
    - https://bugzil.la/1204159
    - https://bugzil.la/1207772

2015-09-25
----------
- loop add-on passes validation, but still no automated signing :/
    - working with folks in #addons
    - turned out to be a bug in the display of errors+warnings
        - https://bugzil.la/1208588
- started google doc to describe/track system-addons build pipeline status
- working on reviewing several new system add-on features
    - https://bugzil.la/1207287
        - done
    - https://bugzil.la/1192926
        - done
    - https://bugzil.la/1193973
    - https://bugzil.la/1204159
    - https://bugzil.la/1207772
- graded more python tests

2015-09-24
----------
- worked on Loop theme issues
    - figured out w/ mossop's help, missing trailing / in manifest :/
- got working x-platform firefox desktop builds w/o built-in loop
    - https://ftp.mozilla.org/pub/mozilla.org/firefox/try-builds/rhelmer@mozilla.com-150066c728b3/
- wrestled with getting loop through the AMO validator

2015-09-23
----------
- put aside taskcluster-github for now
    - it'll be really handy, when it supports x-platform firefox desktop builds
- worked on getting my patch going under try server

2015-09-22
----------
- got a working desktop build from taskcluster-github
    - standard firefox-desktop docker image not quite working
        - symbol upload failing etc.

2015-09-21
----------
- worked on build pipeline prototype for Go Faster
    - using taskcluster-github integration
    - pushed my repo + patch to https://github.com/mozilla/system-addons
- TAG meeting

2015-09-18
----------
- advised on reports monitoring
    - https://bugzil.la/1205336
- started working on getting my moz-central fork building under taskcluster

2015-09-17
----------
- 1:1
- helped out w/ Socorro reporting and monitoring
    - monitoring set up before the AWS move is being phased out
    - making more things that work under simple third-party monitoring svcs

2015-09-16
----------
- still getting over cold
- helped out with Socorro reports problem
    - https://bugzil.la/1205336
- graded more python tests

2015-09-15
----------
- Go Faster meeting
- reviewed system add-on update patch
    - https://bugzil.la/1192924
- out sick in afternoon

2015-09-14
----------
- sick today, sort-of working
- worked w/ jp on build pipeline
- graded python tests
- reviewed patch to fix themes being disabled after addon update/install
    - https://bugzil.la/1204012

2015-09-11
----------
- PTO

2015-09-10
----------
- Started helping out with system add-on build pipeline prototype
    - worked on getting loop tests working in browser/extensions/loop
    - looked into what we want taskcluster to do:
        - regular firefox build + upload
        - run loop marionette tests
        - if test pass:
            - upload to AMO for signing+hosting
            - update balrog with update info
- Took a look at crash correlations
    - https://bugzil.la/1196598

2015-09-09
----------
- Worked on Hello prototype add-on
    - moved themes into add-on
        - still some OS-specific work to do, seems OK on Mac now
    - pushed to bitbucket
        - https://bitbucket.org/rhelmer/mozilla-central
    - updated bug
        - https://bugzil.la/1186172
- cleaned up local hg workspace
- worked on bug about Firefox deleting invalid proxy add-ons
    - https://bugzil.la/1195353

2015-09-08
----------
- Go Faster meeting
- helped out with Socorro correlations reports being late
    - came up with plan for monitoring w/ peterbe+jp
    - discussed getting deploy steps right on stage
    - backfilling ongoing
        - https://bugzil.la/1196598
- review for system add-on signing
    - https://bugzil.la/1192930
- ported a test add-on to Web Extensions API
    - noticed panel is in the wrong place, same as current Add-on SDK
        - https://bugzil.la/1199052
        - discussed w/ billm in IRC - probably should make opening in menu
          the default for browserAction API if the button has been moved into
          the menu, with an optional argument to have a custom panel
    - found bug with browserAction API (missing context menu entries)
        - filed https://bugzil.la/1202862
- started working on bug about Firefox deleting invalid proxy add-ons
    - https://bugzil.la/1195353

2015-09-03
----------
- PTO

2015-09-02
----------
- Done with system add-ons review
    - https://bugzil.la/1192921
    - r+, nothing serious, testing all went fine
- Reviewed Socorro symbol re-encoding PR
    - https://github.com/mozilla/socorro/pull/2978

2015-09-02
----------
- Still working on system add-ons review
    - https://bugzil.la/1192921
    - finished reviewing code, mostly testing

2015-09-01
----------
- Still working on system add-ons review
    - https://bugzil.la/1192921
    - re-read PRD, following update discussion
    - testing with a dumb simple add-on
        - going to test w/ the prototype Loop add-on once that's working
- Go Faster meeting
- 1:1

2015-08-31
----------
- Worked on review for system add-ons changes
    - https://bugzil.la/1192921

2015-08-28
----------
- PTO

2015-08-27
----------
- Updated Loop prototype bug with progress
    - https://bugzil.la/1186172
- Worked on moving final bits from ./browser to add-on
    - browser/theme/loop
        - mostly done, need to put in a bunch of OS version-specific overrides
    - about:loop page registration
        - getting a crash in about:loopconversation :/
            - generated symbols and got a stack, may have to bust out lldb
- finally got around to making a test case and filing max-tabs add-on crash
    - https://github.com/cheeaun/max-tabs/issues/21

2015-08-26
----------
- Loop Add-on totally working \o/
    - shared a video with interested folks
    - spent most of the day testing
- sent and responded to email on go-faster list

2015-08-25
----------
- Go Faster meeting
- Loop Add-on button works, panel opens
    - something still off about the about: -> chrome:// hookup
- circulated doc on challenges of Loop-as-addon
    - lots of follow-up discussion

2015-08-24
----------
- put up patch for removing #ifdefs from UITour.jsm
    - https://bugzil.la/1195962
    - r+ and landed!
- worked on moving loop code to add-on, monorepo-style
    - https://bitbucket.org/rhelmer/mozilla-central
    - no longer using SDK
    - re-using pretty much all the existing code
    - button appears but doesn't quite work yet
        - just need to inject mozLoopAPI

2015-08-21
----------
- patch for install.rdf preference landed
    - first patch in mozilla-central/toolkit authored by me \o/
    - https://bugzil.la/1196301
- backfill for correlations being broken
    - discussed monitoring options w/ jp, maybe consul service check?
- worked on removing loop from browser, reimplementing as add-on
    - I think this is a better approach than the "chrome override" add-on
    - updated https://bugzil.la/1186172#c6 with latest thoughts

2015-08-20
----------
- started google doc exploring external libraries/frameworks/etc.
    - found some preliminary answers about react.js in particular
- looked into why MozReview didn't work for https://bugzil.la/1196301
    - was because I uploaded patch view review board web interface
- set up hg tools like mozreview/bugzilla plugins
- crash correlations not running
    - https://bugzil.la/1196598
    - turned out that analysis node is under-spec'd, causing other troubles

2015-08-19
----------
- patch for add-on manager bug (prefer install.rdf to manifest.json)
    - https://bugzil.la/1196301
- worked on setting up hg+bz+rb integration

2015-08-18
----------
- self-triage (unassigned and closed old self-assigned bugs)
- investigated add-on manager bug (possible signing bug w/ proxy add-on)
    - https://bugzil.la/1195353
- Go Faster meeting

2015-08-17
----------
- helped out w/ symbols/reprocessing for Firefox iOS crashes
    - https://bugzil.la/1178888
- reprocessed Thunderbird crashes for missing symbols
    - https://bugzil.la/1194989#c5

2015-08-14
----------
- helped out w/ Socorro bugs
    - got peterbe access to run ./manage.py
    - ADI now works on stage \o/
    - restored prod DB snapshot on stage

2015-08-13
----------
- crash-analysis node needed some attention
    - https://bugzil.la/1193946
    - https://bugzil.la/1194331
- moar stage Socorro ADI work
    - hopefully the last of it - socorro-adi needs code update
        - this is RHEL6 and can't use the standard Socorro RPM :/

2015-08-12
----------
- Socorro meeting
- urgent symbols bug https://bugzil.la/1193841
- temp fix for bad cert on crash-analysis https://bugzil.la/1193946

2015-08-11
----------
- Go Faster meeting
- 1:1
- reviewed https://github.com/mozilla/socorro/pull/2945

2015-08-10
----------
- investigated what's needed to get prototype loop add-on totally working
    - can we override about: handlers?
    - if not:
        - chrome overrides
        - replace button
            - I think this is needed, to inject mozLoopAPI
- filed Socorro bug 1192869
- looked into Socorro stage issues, blocking ADI work
    - Django just needed to allow crash-stats.allizom.org
- ADI still not working for Socorro stage

2015-08-07
----------
- checked on Socorro ADI - working for prod, not for stage still
    - manually copied ADI over for now
- helped out with a few urgent Socorro bugs
    - https://bugzil.la/1192386
    - https://bugzil.la/1192380

2015-08-06
----------
- meeting about go faster + l10n
- basic chrome override approach working in loop prototype
    - doesn't work yet for JS which expects navigator.{mozLoop, L10n}
- Socorro stage ADI push still not working, loaded config for peterbe

2015-08-05
----------
- worked on loop prototype, uploaded to github
    - https://github.com/rhelmer/loop-addon
- Socorro meeting

2015-08-04
----------
- Go Faster meeting
- add-ons manager review for https://bugzil.la/1190966
- PG disk space getting low in Socorro, commented in https://bugzil.la/1191006
- chatted w/ standard8 and mossop about loop prototype

2015-05-27
----------
- Socorro meeting
    - went over AWS migration and current PHX production issues
- tested RDS migration (production)
- fought fires
    - bug 1156961 - put up PR, so ftpscraper handles 38.0.5b99

2015-05-26
----------
- tested RDS migration (production)
- fought fires
    - bug 1168511 - bad JSON causing trouble in Postgres, blocking crontabber
    - bug 1156961 - put up PR, so ftpscraper handles 38.0.5b99
- landed a few socorro-infra PRs
    - https://github.com/mozilla/socorro-infra/pull/133
    - https://github.com/mozilla/socorro-infra/pull/124
- went into office, replaced Macbook power adapter

2015-05-21
----------
- reviewed phrawzty's ES AWS PR
- practiced RDS migration (stage)
    - going to turn off access until "core" transfer is done
        - current partitions are now part of "core"
    - PHX processors can write to AWS rabbitmq when datastores are sync'd enough

2015-02-24
----------
- progress on S3 symbol storage
    - packaged snappy (symbolapi.m.o)
    - tested S3 symbol upload on stage w/ ted

2015-01-06
----------
- found small % of crashes not being processed
    - bug 1118269
    - reviewed fix https://github.com/mozilla/socorro/pull/2549
- looked into FTP scraping problem
    - bug 1118224
- filed bug(s) to move Socorro to AWS
    - tracking bug 1118288

2015-01-05
----------
- shut down hbase, on S3 only now \o/
- shipped release to fix logging issue that was breaking nagios monitor

2015-01-02
----------
- tracked down date-dependent unittest bug
    - bug 1117250

2014-12-16
----------
- worked on Socorro HBase-to-S3 move
    - pushed production config live
- pushed graphserver update
    - bug 1021842

2014-12-15
----------
- worked on Socorro HBase-to-S3 move
    - production sync finished

2014-12-12
----------
- PTO

2014-12-11
----------
- worked on Socorro HBase-to-S3 move

2014-12-10
----------
- worked on Socorro HBase-to-S3 move

2014-12-09
----------
- worked on Socorro HBase-to-S3 move
    - configured Socorro staging to use HBase as crash source
        - bug 1108974
    - configured Socorro prod to store in S3 alongside hbase
        - bug 1108977
    - asked tmary to start sync/backfill (ETA ~1 week)
    - worked on test plan+scripts for when backfill is complete

2014-12-08
----------
- PTO

2014-12-01 through 2014-12-06
-----------------------------
- mozlandia workweek

2014-11-26
---------------
- reviewed AUS patch
    - bug 1102283
- skipped elmo meeting
- socorro meeting
- tested new "missing symbols" table on stage
    - still a few followups, bug 948644

2014-11-25
---------------
- PTO

2014-11-24
---------------
- tested S3 sync w/ tmary
    - Socorro expects a "dump names" object as well
    - researched compression options

2014-11-21
---------------
- interviewed potential DXR interns
- discussed S3 sync w/ tmary

2014-11-20
---------------
- helped review+test AUS patch in bug 1102283
    - first had to spin up new staging box, bug 1102413
- moar reviews+discussion on S3 for socorro blockers

2014-11-19
---------------
- elmo meeting
    - pushed bbot-ES change live \o/
- socorro meeting
- continued work on blockers to making S3 live
    - reviewed bug 1093888 to get middleware+S3 working
        - worked on related config

2014-11-18
---------------
- continued work on blockers to making S3 live
    - bug 948644 PR# 2487
    - bug 1098954 PR# 2485
- worked with cyliang on using knapsack to copy l10n ES indexes
    - now working \o/
- reviewed graphserver patch to enable geometric mean in UI
    - bug 1077177
- deployed graphserver code for above
    - bug 1101156

2014-11-17
---------------
- worked on blockers to making S3 live
    - bug 948644
    - bug 1098954

2014-11-14
---------------
- collection + processing using S3 is live on socorro stage

2014-11-13
---------------
- worked on debugging socorro S3 stage
- looked into why ES knapsack plugin isn't working for l10n
    - looks like zeus timeouts

2014-11-12
---------------
- worked on getting S3 going on socorro stage
- look into a10n hang (prod)
    - ended up restarting, should try debugging w/ gdb next time
        - https://wiki.python.org/moin/DebuggingWithGdb

2014-11-11
---------------
- elmo meeting
    - worked out plan for pushing ES live today/tomorrow
- socorro meeting
- starting working on enabling S3 in Socorro stage (bug 1097916)

2014-11-10
---------------
- met with ted/lonnen about symbol storage in S3
    - decided to tackle crashstorage this q, symbols next
        - symbols have longer, more complex dependency chain

2014-11-09
---------------
- worked on and withdrew Socorro encryption class
    - boto should be able to handle encryption in transit

2014-11-05
---------------
- worked on graphserver issue w/ jmaher
    - data problem, jmaher fixed
    - graphserver no longer blows up on invalid data, bug 1094029
        - pushed in bug 1094308

2014-11-04
---------------
- finished up bug 1093289
- 1:1
    - took on encrypt/decrypt blobs bug
- graphserver blow-up, bug 1094029


2014-11-04
---------------
- worked on broken correlations (broken by pipe-dump-to-JSON switch)
    - bug 1093289

2014-10-22
---------------
- Socorro meeting
- watched lars make the collector config transition

2014-10-16
---------------
- Elmo meeting

2014-10-14
---------------
- helped w/ graphserver reviews+release
- moving bbot to a10n workers

2014-09-17
---------------
- elmo meeting (canceled)
- helped test bouncer innodb transition
- socorro reviews

2014-05-12
---------------
- elmo meeting
- roll back raven on a10n
    - https://bugzil.la/960304

2014-05-09
---------------
- intro to inventory from uberj
- looked into why some b2g signatures have empty reports tab
    - http://bugzil.la/1002492
- started working on adu-by-signature followup
    - http://bugzil.la/1007379
- started working on middleware for new correlations tables
    - http://bugzil.la/984960

2014-05-08
---------------
- reviewed raven rollback bug
    - http://bugzil.la/960304
- filed follow on adu-by-signature bug
    - http://bugzil.la/1007379

2014-05-07
---------------
- migrated a10n to new database
    - http://bugzil.la/915732

2014-05-05
---------------
- fixed bug in correlations

2014-04-28
---------------
- more progress on getting tests going for tuxedo/bouncer
- landed correlations
- landed adu-by-signature middleware

2014-04-26
---------------
- start of releng workweek

2014-03-24
---------------
- start of webeng workweek
- l10n/elmo meeting
    - fix logging in a10n https://bugzil.la/987203
    - look on/work on http://pike.github.io/a10n/design/

2014-01-28
---------------
- socorro
    - fix regression in topcrasher-by-bug report

2014-01-27
---------------
- socorro
    - landed UI fixes for topcrasher-by-bug report
- elmo
    - followed up w/ jd about new a10n server
        - posted more detailed into to bug

2014-01-24
---------------

2014-01-23
---------------
- socorro
    - fixed TCBS cache problem
        - https://bugzilla.mozilla.org/show_bug.cgi?id=963236

2014-01-22
---------------
- dashcon
- socorro
    - fixed correlation reports

2014-01-21
---------------
- dashcon

2014-01-20
---------------

2014-01-17
---------------

2014-01-16
---------------
- class
- etherpad
    - shipping bug unblocked
    - finding out if current sec review is sufficient to skip
- socorro
    - looking into correlations problems
        - https://bugzilla.mozilla.org/show_bug.cgi?id=947021

2014-01-15
---------------
- etherpad
    - waiting for sec/ops clearance to launch

- socorro
    - meeting
        - decided to take PR 1762
            - needs moar testing
    - reviews

2014-01-14
---------------
- bouncer
    - more work on tuxedo tests
        - most API test failures seem to be due to auth problem
    - fixed issue w/ unreadable API docs
        - missing markup
        - vendor lib needs some work, pretty out of date
- etherpad-lite
    - got ep+mysql working on stackato stage
    - soft-launch empty install on prod?

2014-01-13
---------------
- bouncer
    - got access to prod data snapshot
    - got bouncer+tuxedo working locally
    - reviewed/merged tuxedo patch from rail to set SSL via API
        - currently on stage
- etherpad-lite
    - updated stackato stage/prod to latest release
    - worked on getting to mysql (only supported prod option right now)

2014-01-10
---------------
- bouncer
    - worked on getting tests running on jenkins
        - chatted w/ wenzel, got the basic infra going
        - need to get test data, filed bug 958756 to get current prod DB dump
- socorro
    - reviews

2014-01-09
---------------
- class
- socorro
    - reviews

2014-01-08
---------------
- bouncer
    - worked on getting tests running on jenkins
- socorro
    - meeting
    - reviews

2014-01-07
---------------
- socorro
    - worked on "topcrash for all signatures of a bug" followups
        - landed one, made progress on another
- bouncer
    - met with brandonsavage re: handover
    - set up CI job for bouncer
        - needs some work to go green https://ci.mozilla.org/job/tuxedo/

2014-01-06
---------------
- l10n
    - meeting
        - follow up w/ IT on new a10n server
        - look into potential hg leak
        - think about goals

2013-12-18
---------------
- socorro
    - meeting
    - discussed bouncer issue
    - worked on UI for "topcrash ranks for all signatures of a bug"
        - https://bugzilla.mozilla.org/show_bug.cgi?id=915373

2013-12-17
---------------
- socorro
    - landed new service + model for "topcrash rank for all signatures of a bug"
        - https://bugzilla.mozilla.org/show_bug.cgi?id=915373

2013-12-17
---------------
- socorro
    - worked on service + model for "topcrash rank for all signatures of a bug"
        - https://bugzilla.mozilla.org/show_bug.cgi?id=915373

2013-12-13
---------------
- socorro
    - worked on service + model for "topcrash rank for all signatures of a bug"
        - https://bugzilla.mozilla.org/show_bug.cgi?id=915373
- out part of day w/ dentist appt

2013-12-12
---------------
- socorro
    - meeting
    - working on "topcrash ranks for all signatures of a bug"
        - https://bugzilla.mozilla.org/show_bug.cgi?id=915373
        - not possible to do w/ SQL alone at this time
        - working on composing using existing API + new SignaturesByBugs

2013-12-11
---------------
- socorro
    - meeting
    - working on SQL query for "topcrash ranks for all signatures of a bug"
        - https://bugzilla.mozilla.org/show_bug.cgi?id=915373

2013-12-10
---------------
- socorro
    - reviews

2013-12-04
---------------
- eddy
    - now working (w/ hardcoded app), publishing to datazilla
        - https://datazilla.mozilla.org/?start=1385580857&stop=1386185657&product=B2G&repository=v1.2&test=stopwatch&page=cold_load_time&graph_search=06ce3291f3e843d4&tr_id=37&graph=Firefox%20OS%201.2.0.0-prerelease&project=marketapps

- etherpad
    - just realized that new migration test VM is ready!
        - https://bugzilla.mozilla.org/show_bug.cgi?id=934660

2013-12-03
---------------
- eddy
    - work on hooking up jenkins hamachi b2g testers

2013-12-02
---------------
- l10n
    - meeting
    - enabled sentry for a10n

2013-11-25
---------------
- l10n
    - meeting
        - coordinate downtime/hg upgrade
        - ping jd re: prod a10n

- socorro
    - reviews

2013-11-19
---------------
- socorro
    - worked on review on automatically install/run script
    - static build of stackwalker

2013-11-18
---------------
- socorro
    - worked on review on automatically install/run script
    - helped w/ stackwalker rollout

2013-11-13
---------------
- socorro
    - meeting
    - tracked down probable cause of signature history bug
        - https://bugzilla.mozilla.org/show_bug.cgi?id=789526

2013-11-12
---------------
- l10n
    - meeting w/ jd and pike, finalizing stage and planning production
        - https://etherpad.mozilla.org/a10n-puppet
        - jd is working on it, will let us know in the next few weeks

2013-11-11
---------------
- socorro
    - reviews
        - https://github.com/mozilla/socorro/pull/1664
        - https://github.com/mozilla/socorro/pull/1663
    - PRs
        - automate setup/run of socorro dev mode
            - https://github.com/mozilla/socorro/pull/1665

- l10n
    - meeting
    - chatted w/ shyam about prod hardware for a10n
        - he is checking into it, seamicro nodes
        - might be different group now
    - set up meeting with hd, pike, rhelmer

2013-10-21
---------------
- socorro
    - reviews
- l10n
    - following up on a10n server warnings

2013-10-22
---------------
- socorro
    - reviews
- l10n
    - a10n server up and running

2013-10-14
---------------
- l10n
    - followed up on why a10n is not queueing/working as expected
    - filed bug to set up a10n user
        - https://bugzilla.mozilla.org/show_bug.cgi?id=926543

2013-10-07
---------------
Summit recovery - got some Socorro refactoring and other misc work in.

2013-10-01
---------------
- l10n
    - followup on a10n VM install (almost done)
- graphserver
    - reviewed and pushed graphserver feature
        - https://bugzilla.mozilla.org/show_bug.cgi?id=903914

2013-09-30
---------------
- l10n
    - meeting
    - finish up a10n install
        - filed bugs to get access to elmo DB
        - installed packages and set up test environment on VM

2013-09-26
---------------
- eddy
    - chatted w/ andym about adding new eddy API to marketplace
        - https://github.com/mozilla/zamboni/commit/88e1236d4ac997b5434bc053538183fdcec0d3ba
        - https://github.com/mozilla/zamboni/blob/88e1236d4ac997b5434bc053538183fdcec0d3ba/mkt/stats/api.py#L190-L194

2013-09-25
---------------
2013-09-24
---------------
2013-09-23
---------------
- eddy
    - meeting w/ davehunt and stephend
- elmo
    - meeting
        - need to finish up a10n VM install

2013-09-20
---------------
- eddy
    - apps show-and-tell
        - https://vreplay.mozilla.com/replay/showRecordingExternal.html?key=hs9K5MBSw9SIYHm
        - feedback generall positive
        - probably more useful to surface to app developers
            - simple to do, working on adjusting PR
    - chatted w/ stephend re: new phones
        - incoming "hamachi" phones are not working w/ b2gperf yet
        - no way to queue incoming requests to jenkins, yet
- socorro
    - reviews

2013-09-19
---------------
- eddy
    - patched b2gperf to handle overriding app name
        - this makes it work with mkt "app_slug" names \o/
- socorro
    - reviews

2013-09-23
---------------
- eddy
    - meeting w/ davehunt and stephend
- elmo
    - meeting
        - need to finish up a10n VM install

2013-09-20
---------------
- eddy
    - apps show-and-tell
        - https://vreplay.mozilla.com/replay/showRecordingExternal.html?key=hs9K5MBSw9SIYHm
        - feedback generall positive
        - probably more useful to surface to app developers
            - simple to do, working on adjusting PR
    - chatted w/ stephend re: new phones
        - incoming "hamachi" phones are not working w/ b2gperf yet
        - no way to queue incoming requests to jenkins, yet
- socorro
    - reviews

2013-09-19
---------------
- eddy
    - patched b2gperf to handle overriding app name
        - this makes it work with mkt "app_slug" names \o/
- socorro
    - reviews

2013-09-18
---------------
- socorro
    - meeting
    - reviews

2013-09-17
---------------
- socorro
    - reviews
    - landed install docs + vagrant reboot
        - https://github.com/mozilla/socorro/pull/1508
    - started working on socorro/b2g release channel bug
        - https://bugzilla.mozilla.org/show_bug.cgi?id=869905

2013-09-16
---------------
- eddy
    - chatted w/ andym re: auth for marketplace API
        - need to set up oauth review user for eddy
    - made marketplace-datazilla JS able to load arbitrary apps
- socorro
    - reviews
    - worked on install docs + vagrant reboot
        - https://github.com/mozilla/socorro/pull/1508

2013-09-12
---------------
- eddy
    - get download app loading on device \o/
    - lots of testing with random apps
        - seems to work!

2013-09-11
---------------
- eddy
    - provide way to query if job is already in the queue
- socorro
    - meeting
    - reviews

2013-09-10
---------------
- eddy
    - hooked up "perf test app" button properly
    - made web service take POST for submissions not GET
    - researched actually loading phone onto device
- socorro
    - helped installer on mailing list
    - filed bug about simplifying vagrant
        - https://bugzilla.mozilla.org/show_bug.cgi?id=914727

2013-09-09
---------------
- eddy
    - added basic "test app" button to perfcharts branch
- l10n
    - meeting
    - working on finishing up a10n deploy

2013-09-06
---------------
- eddy
    - started marketplace review dashboard integration
- graphserver
    - pushed minor fix for b2g-inbound hg repo links
        - https://bugzilla.mozilla.org/show_bug.cgi?id=913636

2013-09-05
---------------
- eddy
    - added flask+celery+rabbitmq support to eddy
        - simple endpoint for marketplace reviewer dashboard to hit
        - celery worker runs test and submits to datazilla
    - trying to figure out why b2gperf does not like my unagi build
        - missing build_revision so will not report to datazilla :/
- socorro

2013-09-04
---------------
- eddy
    - published repo with eddy-specific work so far
        - https://github.com/rhelmer/eddy
- socorro
    - meeting, post-mortem
    - backfilling for "corrupted modulelist output" bug
        - https://bugzilla.mozilla.org/show_bug.cgi?id=907280

2013-09-03
---------------
- eddy
    - worked on REST service for launching b2gperf tests from marketplace
- socorro
    - worked on "corrupted modulelist output" bug with harsha
        - https://bugzilla.mozilla.org/show_bug.cgi?id=907280

2013-08-30
---------------
- graphserver
    - helped with graphserver db archiving
        - https://bugzilla.mozilla.org/show_bug.cgi?id=911215

2013-08-29
---------------
- socorro
    - filed bug on update tcbs problem
        - https://bugzilla.mozilla.org/show_bug.cgi?id=910820

2013-08-28
---------------
- eddy
    - got b2gperf running w/ andym's stopwatch app
    - sent email re: next steps
- socorro
    - put up PR for fakedata bug
        - https://bugzilla.mozilla.org/show_bug.cgi?id=909469
    - put up PR to fix b2g scraping problem
        - https://bugzilla.mozilla.org/show_bug.cgi?id=910385
- release-api
    - solarce working on putting standalone scraper on generic cluster
        - https://bugzilla.mozilla.org/show_bug.cgi?id=909902
- graphserver
    - chatted w/ bz about graphserver feature request
        - https://bugzilla.mozilla.org/show_bug.cgi?id=910282

2013-08-27
---------------
- eddy
    - start testing b2gperf with third-party packaged apps
        - https://github.com/mozilla/b2gperf
        - flashed unagi w/ marionette
        - still working on getting b2gperf going

- graphserver
    - reviewed sorting patch
        - https://bugzilla.mozilla.org/show_bug.cgi?id=641414

2013-08-26
---------------
- socorro
    - filed followup bugs from workweek
    - promoted split-out ftp scraper to other teams, #ateam is interested
        - https://github.com/rhelmer/releases
- etherpad-lite
    - investigated spellcheck request
        - https://bugzilla.mozilla.org/show_bug.cgi?id=909352
        - https://github.com/ether/etherpad-lite/issues/1863
        - https://github.com/mozilla/pad/pull/3
    - chatted about hand-off, launching MVP etc.

2013-08-19 - 2013-08-23
---------------
- socorro
    - stability workweek
    - extracted ftpscraper from socorro to standalone service
        - http://releases.paas.allizom.org/
        - https://github.com/rhelmer/releases

2013-08-14
---------------
- socorro
    - followup bug from yesterday's PR
        - https://bugzilla.mozilla.org/show_bug.cgi?id=905642

2013-08-13
---------------
- elmo
    - testing a10n setup
        - discussed deploy script w/ erikrose
            - https://bugzilla.mozilla.org/show_bug.cgi?id=903701
            - erik forked out https://github.com/erikrose/shiva
- socorro
    - worked on table count bug
        - https://bugzilla.mozilla.org/show_bug.cgi?id=898432
        - put up PR https://github.com/mozilla/socorro/pull/1401
    - helped out with missing ADI backfill
        - https://bugzilla.mozilla.org/show_bug.cgi?id=904091
- graphserver
    - followed up on contribution
        - https://bugzilla.mozilla.org/show_bug.cgi?id=688534

2013-08-12
---------------
- elmo
    - weekly meeting
    - looked into elmo test failure
        - turns out was failing on jenkins too but reported as passed!
    - followed up on bugs from Friday w/ Axel

2013-08-09
---------------
- elmo
    - got a10n starting under supervisord
    - filed bugs to track changes so far
        - https://bugzilla.mozilla.org/show_bug.cgi?id=903667
        - https://bugzilla.mozilla.org/show_bug.cgi?id=903670
        - https://bugzilla.mozilla.org/show_bug.cgi?id=903673
    - filed bug to track (continuous) deployment script
        - https://bugzilla.mozilla.org/show_bug.cgi?id=903701
    - filed bug about puppetizing a10n VM
        - https://bugzilla.mozilla.org/show_bug.cgi?id=903702
    - bugs in a10n twistd app that block deployment
        - https://bugzilla.mozilla.org/show_bug.cgi?id=903703
        - https://bugzilla.mozilla.org/show_bug.cgi?id=903704
    - tracker bug for deploying new VM
        - https://bugzilla.mozilla.org/show_bug.cgi?id=903705

2013-08-08
---------------
- eddy
    - submitted test data via `datazilla_client`
- elmo
    - got a10n working in local dev env
    - working on startup scripts (supervisord)
- socorro
    - email/irc chatter about dev/stage data sync issues


2013-08-07
---------------
- elmo
    - figuring out bugs in test setup script
    - worked out plan for standard deployment script w/ ErikRose
- socorro
    - weekly meeting
    - answer random irc queries :)

2013-08-06
---------------
- elmo
    - discussed deployment strategy w/ solarce
    - local VM issues, plowed through
- socorro
    - PR to speed up socorro-vagrant jenkins job
        - https://github.com/mozilla/socorro/pull/1387
        - 1h20m -> ~40m

2013-08-05
---------------
- elmo
    - attended elmo meeting
    - went over a10n test setup w/ axel
        - http://pike.github.io/a10n/test-setup/
        - now working locally
- socorro
    - reviewed https://github.com/mozilla/socorro/pull/1382

2013-08-02
---------------
- eddy
    - chatted w/ ctalbert about running tests
        - followup w/ stephend + davehunt on Monday
    - reviewed info jeads sent a while back for testing /marketapps endpoint
- socorro
    - helped peterbe w/ webapp-django -> devdb
    - helped out w/ configman mware setup

2013-07-31
---------------
- graphserver
    - shipped y-axis patch (https://bugzil.la/641413)

2013-07-30
---------------
- elmo
    - got working settings/local.py from Pike, will contribute fixes
      for local.py-dev so others do not trip on yesterday's problems
- socorro
    - reviewed https://github.com/mozilla/socorro/pull/1375
    - investigated https://bugzil.la/898432

2013-07-29
---------------
- elmo
    - weekly meeting
    - helped look at jenkins test failure, filed https://bugzil.la/899160
    - continued puppet and basic setup in vagrant VM
        - plan to hand this basic puppet setup off to IT for new prod VM setup
        - does not start up - seems to not be finding settings/local.py
- eddy
    - merged perfcharts branch to latest https://github.com/rhelmer/zamboni
    - got zamboni running on new laptop
- socorro
    - reviews
        - https://github.com/mozilla/socorro/pull/1370
        - https://github.com/mozilla/socorro/pull/1373
- graphserver
    - sent email to dev-planning about upcoming y-axis feature
        - has been in the pipeline for months, recently unblocked
- pushlog
    - did some analysis on access logs for load-testing purposes

2013-07-28
---------------
- socorro
    - chatted w/ socorro installer
        - got them interested in my Go collector/processor :)

2013-07-26
---------------
- elmo
    - more work on a10n VM puppet manifests
- eddy
    - started beating zamboni patch into shape
- socorro
    - helped mjrosenb w/ ad-hoc query
    - picked up bad fix of mine https://bugzil.la/898432
- graphserver
    - helped mbrubeck pick up some volunteer tasks, until datazilla is ready
        - removed index page https://bugzil.la/898640
        - finished out https://bugzil.la/835751 for sheeri
        - pushed three releases (v2.3.8, v2.3.9 and v2.3.10)

2013-07-25
---------------
- elmo
    - worked on puppet for a10n VM
- eddy
    - SfN meeting, nothing to report
- socorro
    - reviews
    - looking at JSON encoding issue w/ kairo
    - helped external user w/ install (oleavr)
- graphserver
    - put up patch for review on perf problems (https://bugzil.la/835751)

2013-07-24
---------------
- elmo
    - worked on access to new a10n VM + puppet w/ rbryce
- eddy
    - delays due to viscosity/tunnelblick problems
- socorro
    - followed up on dev and vagrant problems (https://bugzil.la/892271)
- graphserver
    - followed up on perf problems https://bugzil.la/835751
    - https://bugzil.la/897580
- etherpad
    - discussions with jakem
    - https://bugzil.la/897693
