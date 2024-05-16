---
title: "Home"
layout: home
nav_enabled: true
collections:
  # Define a collection named "tests", its documents reside in the "_tests" directory
  security:
    permalink: "/:collection/:security/"
    output: true

just_the_docs:
  # Define which collections are used in just-the-docs
  collections:
    # Reference the "tests" collection
   security:
      # Give the collection a name
      name: security
      # Exclude the collection from the navigation
      # Supports true or false (default)
      # nav_exclude: true
      # Fold the collection in the navigation
      # Supports true or false (default)
      # nav_fold: true  # note: this option is new in v0.4
      # Exclude the collection from the search
      # Supports true or false (default)
      # search_exclude: true
---



