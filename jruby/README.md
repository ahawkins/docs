# Supported tags and respective `Dockerfile` links

- [`1.7`, `1.7.16`, `1.7.16.1`, `latest` (*1.7/Dockerfile*)](https://github.com/cpuguy83/docker-jruby/blob/fe814254b51c4f619ec2561df421259c32b27c63/1.7/Dockerfile)
- [`dev` (*9000/Dockerfile*)](https://github.com/cpuguy83/docker-jruby/blob/384671d2c1b26465a38c6f9e645024b3ab217bad/9000/Dockerfile)
- [`1.7-onbuild`, `1.7.16-onbuild` (*1.7/onbuild/Dockerfile*)](https://github.com/cpuguy83/docker-jruby/blob/10eae9359611104c013e82206104b40f20fac377/1.7/onbuild/Dockerfile)

For more information about this image and its history, please see the [relevant
manifest file
(`library/jruby`)](https://github.com/docker-library/official-images/blob/master/library/jruby)
in the [`docker-library/official-images` GitHub
repo](https://github.com/docker-library/official-images).

# What is JRuby?

JRuby (http://www.jruby.org) is an implementation of Ruby
(http://www.ruby-lang.org) on the JVM.

Ruby is a dynamic, reflective, object-oriented, general-purpose, open-source
programming language. According to its authors, Ruby was influenced by Perl,
Smalltalk, Eiffel, Ada, and Lisp. It supports multiple programming paradigms,
including functional, object-oriented, and imperative. It also has a dynamic
type system and automatic memory management.

> [wikipedia.org/wiki/Ruby_(programming_language)](https://en.wikipedia.org/wiki/Ruby_(programming_language))

JRuby leverages the robustness and speed of the JVM while providing the same
Ruby that you already know and love.
With JRuby you are able to take advantage of real native threads, enhanced
garbage collection, and even import and use java libraries.

![logo](https://raw.githubusercontent.com/docker-library/docs/master/jruby/logo.png)

# How to use this image

## Create a `Dockerfile` in your Ruby app project

    FROM jruby:1.7-onbuild
    CMD ["./your-daemon-or-script.rb"]

Put this file in the root of your app, next to the `Gemfile`.

This image includes multiple `ONBUILD` triggers which should be all you need to
bootstrap most applications.  The build will `COPY . /usr/src/app` and `RUN
bundle install`.

You can then build and run the Ruby image:

    docker build -t my-ruby-app .
    docker run -it --name my-running-script my-ruby-app

### Generate a `Gemfile.lock`

The `onbuid` tag expects a `Gemfile.lock` in your app directory. This `docker
run` will help you generate one. Run it in the root of your app, next to the
`Gemfile`:

    docker run --rm -v "$(pwd)":/usr/src/app -w /usr/src/app jruby:1.7 bundle install --system

## Run a single Ruby script

For many simple, single file projects, you may find it inconvenient to write a
complete `Dockerfile`. In such cases, you can run a Ruby script by using the
Ruby Docker image directly:

    docker run -it --rm --name my-running-script -v "$(pwd)":/usr/src/myapp -w /usr/src/myapp jruby:1.7 jruby your-daemon-or-script.rb

# License

View [license information](https://github.com/jruby/jruby/blob/master/COPYING)
for the software contained in this image.

# User Feedback

## Issues

If you have any problems with or questions about this image, please contact us
 through a [GitHub issue](https://github.com/cpuguy83/docker-jruby/issues).

You can also reach many of the official image maintainers via the
`#docker-library` IRC channel on [Freenode](https://freenode.net).

## Contributing

You are invited to contribute new features, fixes, or updates, large or small;
we are always thrilled to receive pull requests, and do our best to process them
as fast as we can.

Before you start to code, we recommend discussing your plans 
through a [GitHub issue](https://github.com/cpuguy83/docker-jruby/issues), especially for more ambitious
contributions. This gives other contributors a chance to point you in the right
direction, give you feedback on your design, and help you find out if someone
else is working on the same thing.
