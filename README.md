# A repo exploring how to setup travis, jekyll and s3 to autopublish a static site from a github repo

## pre-requisites

 * Ruby (to run jekyll and gem install the dependencies)
 * Git client (to push updates to a github repo)

## Installation

Run `. ./script/init test-site` to initialise the local build. (If you want to name the site something else then `rm -rf` the `test-site` folder and call the `init` method with the new site name as the argument.

Then run `setup` to setup jekyll and create a new jekyll site.

## Commands

Note: to run any commands in a shell, you must run the `. ./script/init test-site` command first to setup the shell correctly.

To run the jekyll site locally run the `run-local` command.
