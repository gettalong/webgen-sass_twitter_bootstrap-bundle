# Sass Twitter Bootstrap framework for webgen

This is a webgen extension bundle that provides the [Sass][1] port of
the [Twitter Bootstrap framework][2]. This allows the easy inclusion of
parts or all of the Twitter Bootstrap framework in webgen websites.

It is based on the great LESS-to-Sass translation
[sass-twitter-bootstrap][3].

[1]: http://sass-lang.com
[2]: http://twitter.github.com/bootstrap/
[3]: https://github.com/jlong/sass-twitter-bootstrap


# Usage

Since this is a port of the Twitter Bootstrap CSS framework to Sass, you
can only use it if you use Sass. The needed Sass stylesheets are
provided under the `/bootstrap/` path. *Note* that the Sass files are
only available to the Sass/Scss content processors, i.e. no nodes are
created for them!

The following statement placed in any Sass stylesheet you use in your
webgen website would import the whole Bootstrap CSS framework:

    @import "/bootstrap/bootstrap"

The Twitter Bootstrap javascript files are provided as passive nodes
under the `/javascripts/` path. Note that they depend on [JQuery], so
the JQuery javascript library needs to be loaded before any of these
files!

[JQuery]: http://jquery.com


# Installation

The easiest way to install this extension bundle is by installing the
corresponding Rubygem:

    gem install webgen-sass_twitter_bootstrap-bundle

If you don't use Rubygems, copy the folder
`lib/webgen/bundle/sass_twitter_bootstrap` into your `ext` directory.

After that you just need to tell webgen to use this extension bundle by
adding the following line to your `ext/init.rb` file:

    load("sass_twitter_bootstrap")


# Copyright and license

Copyright 2012 Thomas Leitner

Licensed under the Apache License, Version 2.0 (the "License"); you may
not use this file except in compliance with the License. You may obtain
a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

* * *

The used files from the sass-twitter-bootstrap repository are licensed
under the Apache License, Version 2 (see
<https://github.com/jlong/sass-twitter-bootstrap#copyright-and-license>).
