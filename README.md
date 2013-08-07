TODO
===============
- l10n tools (Mon-Tue)
    - https://github.com/rhelmer/a10n/compare/puppet
    - help set up new VM w/ puppet
    - continue setting up a10n locally
        - contribue settings fixes to local.py-dev
- eddy (Wed-Fri)
    - https://github.com/rhelmer/zamboni/compare/perfcharts
    - set up test jobs on QA jenkins
        - bug stephend/davehunt on Mondy
    - talk w/ marketplace folks about perfcharts branch
- pushlog
    - http://hg.mozilla.org/users/rhelmer_mozilla.com/pushlog
    - load testing for http://bugzil.la/827123
    - read hg docs
        - http://mercurial.selenic.com/wiki/Revlog
        - http://mercurial.selenic.com/wiki/WritingExtensions
- etherpad
    - https://github.com/rhelmer/etherpad-lite
    - work on migrating data to postgres
    - figure out URL redirects for old team sites
    - remaining security blockers
- socorro
    - fix regression https://bugzil.la/898432

- make video of webtools workflow
    - compare/contrast hg/tryserver/etc.

STABILITY WORKWEEK TOPICS
---------------

- "lack of data" problem
- deprecating socorro-dev@ in favor of tools-socorro@ and stability@
- making dev env better
    - strip down vagrant/puppet, add multi-machine support

DONE
===============
2013-08-03
---------------
- eddy
- elmo

2013-08-03
---------------
- elmo
    - discussed deployment strategy w/ solarce
    - local VM issues, plowed through
- socorro
    - PR to speed up socorro-vagrant jenkins job
        - https://github.com/mozilla/socorro/pull/1387
        - 1h20m -> ~40m

2013-08-02
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
