TODO
===============
- eddy (Wed-Fri)
    - https://github.com/rhelmer/eddy
    - https://github.com/rhelmer/zamboni/compare/perfcharts
    - talk w/ marketplace folks about reviewing perfcharts branch
    - figure out why b2gperf will not publish to datazilla
        - cannot find build/gaia/etc revision?
        - hacked around for now
    - figure out how eddy should use auth against API to get manifest/zip
        - getting back 'You do not own that app.' for unreviewed apps
    - zamboni needs app slug, and b2gperf only handles app name
        - there may be multiple apps w/ same name but different slugs
        - not sure what happens if there are multiple such apps on the phone?
            - try stopwatch
- pushlog
    - `http://hg.mozilla.org/users/rhelmer_mozilla.com/pushlog`
    - load testing for http://bugzil.la/827123
    - read hg docs
        - http://mercurial.selenic.com/wiki/Revlog
        - http://mercurial.selenic.com/wiki/WritingExtensions
- l10n tools (Mon-Tue)
    - https://github.com/rhelmer/a10n/compare/bug903673-puppetize-a10n
    - tracking bug
        - https://bugzilla.mozilla.org/showdependencytree.cgi?id=903705
    - help set up new VM w/ puppet
    - continue setting up a10n locally
        - contribute settings fixes to local.py-dev
- socorro
- etherpad
    - https://github.com/rhelmer/etherpad-lite
    - work on migrating data to postgres
    - figure out URL redirects for old team sites
    - remaining security blockers

misc
    - make video of webtools workflow
        - compare/contrast hg/tryserver/etc.
    - public version of eddy
    - get socorro working in little docker containers

STABILITY WORKWEEK TOPICS
---------------

- "lack of data" problem
- deprecating socorro-dev@ in favor of tools-socorro@ and stability@
- making dev env better
    - strip down vagrant/puppet, use centos to be more like mozilla production

DONE
===============

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
