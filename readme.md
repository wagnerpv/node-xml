# XML for Node

  Fast and simple Javascript-based XML generator/builder for Node projects.

## Install

   $ npm install xml

## Examples

 There are examples in the examples directory.

## Tests

 Use [nodeunit](https://github.com/caolan/nodeunit) to run the tests.

    $ npm install nodeunit
    $ nodeunit test

Everything should pass:

    test
    ? empty
    ? simple
    ? deep
    ? indent
    ? attributes
    ? cdata
    ? encoding

    OK: 30 assertions (4ms)

## API
    XML(object, [indent])

  * __object__ See Usage for how this can work.
  * __indent__ Falsy value: No indent or line breaks (default). True: 4 spaces. '\t': Single tab. '  ': Two spaces.  Etc.

## Usage

    var XML = require('xml');

    var example1 = [ { url: 'http://www.google.com/search?aq=f&sourceid=chrome&ie=UTF-8&q=opower' } ];
    console.log(XML(example1));
    //<url>http://www.google.com/search?aq=f&amp;sourceid=chrome&amp;ie=UTF-8&amp;q=opower</url>

    var example2 = [ { url: { _attr: { hostname: 'www.google.com', path: '/search?aq=f&sourceid=chrome&ie=UTF-8&q=opower' }  } } ];
    console.log(XML(example2));
    //<url hostname="www.google.com" path="/search?aq=f&amp;sourceid=chrome&amp;ie=UTF-8&amp;q=opower"/>

    var example3 = [ { toys: [ { toy: 'Transformers' } , { toy: 'GI Joe' }, { toy: 'He-man' } ] } ];
    console.log(XML(example3));
    //<toys><toy>Transformers</toy><toy>GI Joe</toy><toy>He-man</toy></toys>
    console.log(XML(example3, true));
    /*
    <toys>
        <toy>Transformers</toy>
        <toy>GI Joe</toy>
        <toy>He-man</toy>
    </toys>
    */

    var example4 = [ { toys: [ { _attr: { decade: '80s', locale: 'US'} }, { toy: 'Transformers' } , { toy: 'GI Joe' }, { toy: 'He-man' } ] } ];
    console.log(XML(example4, true));
    /*
    <toys decade="80s" locale="US">
        <toy>Transformers</toy>
        <toy>GI Joe</toy>
        <toy>He-man</toy>
    </toys>
    */

    var example5 = [ { toys: [ { _attr: { decade: '80s', locale: 'US'} }, { toy: 'Transformers' } , { toy: 'GI Joe' }, { toy: [ { name: 'He-man' }, { description: { _cdata: '<strong>Master of the Universe!</strong>'} } ] } ] } ];
    console.log(XML(example5, true));
    /*
    <toys decade="80s" locale="US">
        <toy>Transformers</toy>
        <toy>GI Joe</toy>
        <toy>
            <name>He-man</name>
            <description>
    <![CDATA[
    <strong>Master of the Universe!</strong>
    ]]>
            </description>
        </toy>
    </toys>
    */


## Keywords

 * ___atr__: set attributes using a hash of key/value pairs.
 * ___cdata__: Value of _cdata is wrapped in xml CDATA so the data does not need to be escaped.


# Contributing

Contributions to the project are most welcome, so feel free to fork and improve.

# License

(The MIT License)

Copyright (c) 2011 Dylan Greene <dylang@gmail.com>

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.