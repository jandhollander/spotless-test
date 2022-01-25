# This repo illustrates a bug in spotless maven plugin

When running mvn spotless:check or spotless:apply, the pom.xml from the
subdirectory isn't taken into account.  
- the parent of sub/pom.xml is pom.xml
- pom.xml defines the configuration of the spotless plugin
  - ratchetFrom: origin/main
  - use sortPom to handle pom files

## Scenario 1: run from root
- edit both **pom.xml** and **sub/pom.xml** to contain eg. a couple of redundant spaces in front of a tag so that sortpom
  would find this file to be malformed
- run **mvn spotless:apply** in the location where the parent pom.xml is located
- notice that only **pom.xml** is flagged as malformed and fixed

## Scenario 2: run from sub
- edit both **pom.xml** and **sub/pom.xml** to contain eg. a couple of redundant spaces in front of a tag so that sortpom
  would find this file to be malformed
- run **mvn spotless:apply** in /sub/
- notice that **no file** is flagged as malformed and fixed

