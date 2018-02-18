# A repo exploring how to setup travis, jekyll and s3 to autopublish a static site from a github repo

## pre-requisites

 * Ruby (to run jekyll and gem install the dependencies)
 * Git client (to push updates to a github repo)

## Installation

Run `. ./script/init test-site` to initialise the local build. (If you want to name the site something else then `rm -rf` the `test-site` folder and call the `init` method with the new site name as the argument.

Then run `setup` to setup jekyll and create a new jekyll site.

## Commands

Note: to run any commands in a shell, you must run the `. ./script/init test-site` command first to setup the shell correctly.

To run the jekyll site locally run the `local:run` command.
To test the jekyll site locally run the `local:test` command.

The travis build script is configured to run the `ci:build` command which will do a jekyll build and run htmlproofer to test the build.

## Brand

https://color.adobe.com/create/color-wheel/?copy=true&base=2&rule=Custom&selected=4&name=Copy%20of%20stickyboard&mode=rgb&rgbvalues=0.05475818619339773,0.291845812960357,0.6000000000000001,0.3536979619362134,0.634729629902792,1,0.22832816574259207,0.5203913881842657,0.9,1,0.7316386210978574,0.22889014679771513,0.9,0.6560627673719788,0.39648089988607216&swatchOrder=0,1,2,3,4

