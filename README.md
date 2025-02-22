# faustpp

[![Build Status](https://travis-ci.com/jpcima/faustpp.svg?branch=master)](https://travis-ci.com/jpcima/faustpp)

A post-processor for faust, which allows to generate with more flexibility

This is a source transformation tool based on the [Faust compiler](https://faust.grame.fr/).

It permits to arrange the way how faust source is generated with greater flexibility.

Using a template language known as [Jinja2](https://jinja.palletsprojects.com/), it is allowed to manipulate
metadata with iteration and conditional constructs, to easily generate custom code tailored for the job.
Custom metadata can be handled by the template mechanism.

## Usage

For detailed information, refer to the [documentation](https://jpcima.github.io/faustpp).

An example is provided in the `architectures` directory.
It is usable and illustrates many features.

The example is able to create a custom processor class. It has these abilities:
- a split generation into a header and an implementation file
- a direct introspection of the characteristics of the controls
- recognition of some custom metadata: `[symbol:]` `[trigger]` `[boolean]` `[integer]`
- named getters and setters for the controls
- a simplified signature for the processing routine

This example can be used to generate any file. Pass options to the Faust compiler using `-X`.
In this particular example, you should pass a definition of `Identifier` in order to name the result class,
which is done with the option `-D`.

```
faustpp -X-vec -DIdentifier=MyEffect -a generic.cpp effect.dsp > effect.cpp
faustpp -X-vec -DIdentifier=MyEffect -a generic.hpp effect.dsp > effect.hpp
```

## Building

To build the software yourself, you may type the following commands, or open the project in your favorite IDE.

```
git clone --recursive https://github.com/jpcima/faustpp.git
cd faustpp
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr ..
cmake --build .
```

And then install (optional):

```
sudo cmake --build . --target install
```
