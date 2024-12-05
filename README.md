# laurenzfg.com
source code for laurenzfg.com, my personal homepage.
This whole thing is a hack, need to redo it some day.
Maybe it is not the smartest thing to use Jekyll if you have never used Ruby
before.

Anyways, full CD is configured using Netlify, so just dump content here til
something explodes.

## Deploy / Compile Guide
Build environment:

    $ gem install bundler
    $ bundle install
    $ bundle exec jekyll serve

Make distribution ready for upload.

    $ bundle exec jekyll build

## Where to put the texts

- `_posts` contains the software projects
- `_config.yml` holds the texts for the hero sections
- `.md` files in the root directory will be converted to "pages" (e.g. `/about`)