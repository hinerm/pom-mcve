# pom-mcve
A minimal test of dependency management overriding when inheriting multiple versions of the same BOM.

This repository models the following project structure:


                    pom-foo
                      * direct
                      * trans
                  /    |    \
                /      |      \
            pom-fizz   |      pom-buzz
              * fizz   |        * buzz
             / \       |        / \
           /    \      |      /    \
       fizz       \    |    /      buzz
         - direct   \  |  /          - direct
         - trans      app            - trans
                        - buzz
                        - fizz
                        - direct


\* indicates a managed version

\- indicates a direct dependency

## Usage

This project allows us to explore the effects on managed versions of
dependencies in multiple-inheritance scenarios, where an application
distributes multiple components and all inherit from the same BOM (with
potentially differing versions).

By default, there are three versions of pom-foo: 1.0, 1.1, 1.2. Each pom-foo version manages different versions of two dependencies.

The down-stream consumers of pom-foo each extend a different pom-foo version. The final app then scope:imports pom-fizz and pom-buzz.

The goal is to understand what exactly we need to test to guarantee compliance between projects with guaranteed dependency skew.

The output of:

  mvn dependency:tree -Dverbose

is included with each project.
