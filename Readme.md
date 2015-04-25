![logo](http://buildkite.github.io/terminal/images/logo.svg)

Terminal is a Go library for converting arbitrary shell output (with ANSI) into beautifully rendered HTML. See http://en.wikipedia.org/wiki/ANSI_escape_code for more information about ANSI Terminal Control Escape Sequences.

It provides a single command, `terminal-to-html`, that can be used to convert terminal output via STDIN, as well as via a simple web server.

[![Build status](https://badge.buildkite.com/20b99da4c5267bad4b1a8b30013b0d3f644b70fbf43039b973.svg)](https://buildkite.com/terminal/terminal)

## Usage

Piping in terminal output via the command line:

``` bash
cat fixtures/pickachu.sh.raw | terminal-to-html -preview > out.html
```

Posting terminal content via HTTP:

```bash
terminal-to-html -http=:6060 &
curl --data-binary "@fixtures/pikachu.sh.raw" http://localhost:6060/terminal > out.html
```

For coloring you can use the sample [terminal.css](/assets/terminal.css) stylesheet and wrap the output in an element with class `term-container` (e.g. `<div class="term-container"><!-- terminal output --></div>`).

### Image support

Terminal has basic support for [iTerm2 inline images](http://iterm2.com/images.html). Only control sequences with `inline=1` will be rendered and `preserveAspectRatio` is not supported.

Terminal also provides a way to refer to images served by your webserver rather than transmitted via ANSI. The format is similar to iTerm2 inline images:

`1338;path=my/image/path.gif;width=100%;height=50px`

Specify `-assets=/path` on the command line to prefix all relative image paths with `/path/`.

## Installation

Download the release for your platform from [https://github.com/buildkite/terminal/releases](https://github.com/buildkite/terminal/releases)

## Manual Installation

Assuming a `$GOPATH/bin` that's globally accessible, run:

```bash
$ go install github.com/buildkite/terminal/cmd/terminal-to-html
```

## Developing

To get a bash prompt with all the go cross-compilation tools set up for you already:

```
$ docker build -t terminal . && docker run -it --rm -v $(pwd):/go/src/github.com/buildkite/terminal terminal bash
```

## Benchmarking

Run `go test -bench .` to see raw Go performance. The `npm` test is the focus: this best represents the kind of use cases the original code was developed against.

## Contributing

1. Fork it ( https://github.com/[my-github-username]/terminal/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request

## Licence

> Copyright (c) 2015 Keith Pitt, Tim Lucas, Michael Pearson
>
> MIT License
>
> Permission is hereby granted, free of charge, to any person obtaining
> a copy of this software and associated documentation files (the
> "Software"), to deal in the Software without restriction, including
> without limitation the rights to use, copy, modify, merge, publish,
> distribute, sublicense, and/or sell copies of the Software, and to
> permit persons to whom the Software is furnished to do so, subject to
> the following conditions:
>
> The above copyright notice and this permission notice shall be
> included in all copies or substantial portions of the Software.
>
> THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
> EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
> MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
> NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
> LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
> OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
> WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
