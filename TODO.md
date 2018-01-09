Things to follow up on
======================

- pref
  - does the way we flip prefs in hotfixes ("defaultBranch") get synced?

- message ursula and marina about prio

- Follow changes related to bootstrapped add-ons
  - ideally these are going away
    - system add-ons could pretty easily move to regular Firefox components
      - no more out-of-band updates, but Firefox updates could be better
    - Shield studies could still work with the right internal webext APIs

- Follow up on Ted's pointers about running updater as standalone rust process
  - look into windows service wrappers
  - find folks to ask about sandboxing
  - useful IPC pointers:
    - probably need different approaches per-OS:
      - Windows - named pipes
      - macOS - mach ports
      - Linux - named pipes or maybe sockets
    - when the update process is started by the app, it's pretty easy

Done
====
- Follow up with Ted re: pingsender
  - e.g. https://bugzil.la/1310703
  - specifically - how about writing an update client in rust,
    that can run standalone on startup, or as a windows service?
    - server based on omaha
    - starting with safer targets like blocklist
    - need to IPC w/ Firefox to notify that updates have landed
      - mach ports on osx
      - unix sockets on linux
      - named pipes (?) on windows
      - if Firefox isn't running, just drop them in
      - what if Firefox is running but doesn't respond?
        - maybe stage updates and install later, when it's back or totally gone?
      - what if there are multiple Firefoxes running under different
        accounts on the same machine?
        - standalone client can handle this but what about the service?

- pre-57 perf wins
  - kill checkForChanges
    - look more specifically at what it does...
