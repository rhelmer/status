TODO
===============
- socorro
    - help w/ AWS move
        - symbol store -> S3
        - crash collection -> S3

- l10n tools (elmo, a10n)
    - remove dependency on buildbot

- bouncer/tuxedo
    - get all tests working on CI

DONE
===============

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
