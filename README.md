## PHPWebBench

PHPWebBench is a tool for executing performance tests of HTTP web applications.
It performs HTTP requests using different methods (GET, POST, PUT, DELETE) and retrieve
information about the response time, the bytes downloaded, the transfer rate, etc.


### INSTALL

In order to install the software you need to use [Composer](http://getcomposer.org/).
You need to execute the following composer command:

```bash
composer install
```

Composer will install the dependencies of the project inside the vendor folder.
After that, you can start to use `PHPWebBench` from the command line using the
`bin/runbench` script.

### USAGE

The `bin/runbench` script can be executed as follows:

```bash
bin/runbench -h
```

Execute a test on a single URL (by default it executes 3 requests using 1 client).

```bash
bin/runbench -u http://url-to-test
```

Execute a test on a single URL using 100 requests and 10 concurrent clients.

```bash
bin/runbench -n 100 -c 10 -u http://url-to-test
```

PHPWebBench can be also used with a PHP configuration file. In the example folder you can
find a configuration file `example/test.php` that contains the following
values:

```php
return [
    [
        'name' => 'Google',
        'url'  => 'http://www.google.com'
    ],
    [
        'name' => 'Yahoo',
        'url'  => 'http://www.yahoo.com'
    ],
    [
        'name' => 'Bing',
        'url'  => 'http://www.bing.com'
    ]
];
```

In order to execute the benchmark test using a configuration file you need to
use the -b option. For instance, to run the example/test.php file:

```bash
bin/runbench -b example/test.php
```

### OUTPUT

The output of the script is a collection of information regarding the performance
results. Below is reported an example of execution:

```
PHPWebBench 0.1a by Enrico Zimuel.

Running test Google...done
Running test Yahoo...done
Running test Bing...done

RESULTS:
--------
Number of requests   : 3
Concurrency level    : 1
Time for tests       : 5.59 sec

Test name            : Google
URL                  : http://www.google.com
Status code 200      : 3
Document size        : 42.38 [Kb]
Total transferred    : 131.62 [Kb]
Requests per second  : 4.10 [#/sec]
Time per request     : 243.57 ± 59.25 [msec] (mean)
Transfer rate        : 180.00 [Kb/sec]

Test name            : Yahoo
URL                  : http://www.yahoo.com
Status code 200      : 3
Document size        : 387.78 [Kb]
Total transferred    : 1.14 [Mb]
Requests per second  : 0.85 [#/sec]
Time per request     : 1180.64 ± 162.32 [msec] (mean)
Transfer rate        : 328.82 [Kb/sec]

Test name            : Bing
URL                  : http://www.bing.com
Status code 200      : 3
Document size        : 31.15 [Kb]
Total transferred    : 97.20 [Kb]
Requests per second  : 2.28 [#/sec]
Time per request     : 439.26 ± 134.62 [msec] (mean)
Transfer rate        : 73.74 [Kb/sec]
```

The information reported in the output are quite similar to the
[Apache benchmark](http://httpd.apache.org/docs/2.2/programs/ab.html) output.

The most important value for performance consideration is the *Time per request*
that give you an idea about the average response time of each HTTP request.

### GRAPH

PHPWebBench can generates the graphs of the results using [gnuplot](http://www.gnuplot.info/).
In order to produce the graphs you need to use the --graph (-g) option, for instance:

```bash
bin/runbench -b example/test.php -g example
```

This command executes the benchmark test in `example/test.php` and generates the
graphs in the `example` folder.

The graphs are generated with a file containing the data to be plotted (a csv
file .dat) and a gnuplot script file (.plt).

The images are generated using the PNG format as default adapter. If you want
you can specify a different file format using the `--gformat` option.
For instance, if you want to generate PostScript files you can use the following
command:

```bash
bin/runbench -b example/test.php -g example --gformat ps
```

PHPWebBench supports the following images formats: png, ps, pdf, jpg, svg, gif.


### LICENSE

The files in this archive are released under the
[BSD 3-Clause License](http://opensource.org/licenses/BSD-3-Clause).
