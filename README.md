TODO
===============
- prototype browser features as system add-ons
    - loop
- support/training on Socorro as needed

DONE
===============
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
