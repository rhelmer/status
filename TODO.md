Things to follow up on
======================

- write up plan for unifying updaters 

- do system add-on updates show up in about:addons if it happens to be loaded?
  - saw it on release (52.0.1) but went away when page reloaded

- pre-57 perf wins
  - kill dir scanning
    - prereq is that there's only one way to install/register addons
      - e.g. windows sideload must use registry
    - linux/mac global dirs can go last, figure something out there
    - bake in list of built-in add-ons (system addons etc)
  - kill checkForChanges
    - look more specifically at what it does...
  - shrink prefs
    - hardcoded abs paths errwhere...

- post-57 perf wins
  - no more loading XUL add-ons
  - kill extensions.ini
