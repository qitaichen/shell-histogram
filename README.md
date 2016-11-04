# Feature #
* to calculate the result of a datetime file 
* to display the histogram result in the console 

# Install #

    # download code
    git clone https://github.com/qitaichen/shell-histogram.git

    cd shell-histogram
    # add the path to shell 
    echo "# add shell histogram to path" >> ~/.bash_profile
    echo "PATH=\$PATH;`pwd`/bin" >> ~/.bash_profile
    source ~/.bash_profile
  

# calculate #
to calculate the result of a datetime, you can choose the time block size, min time block is one minute.

## input/output file format ##
two file format is allow:
    
    2016-01-01 12:01:01,1
    2016-01-01 12:11:08,4

or 

    2016-01-01 12:01:01
    2016-01-01 12:11:08

* every datetime item should be one line 
* if the num is empty, use 1 as default


## output file format ##
the same as input file 
    
## Usage ##

    Usage: histogram_cal [options]
      to cal the histogram result
      e.g: histogram_cal -f file.test -n 60

    Options: 
      -h/--help       to see the help
      -f/--file       file name: the input file name, should be result of histogram prepare
      -n/--block-num  min block num: how many min you would merge to a block


# histogram show #
to display the result in the console

## input file format ##
the same as calculate input file

## usage ##

    Usage: histogram_show [options]
      e.g: histogram_show -f file.test -c 30

    Options:
      -h/--help       to see the help
      -f/--file   file name: the input file, if the file name is empty, read from standard input
      -c/--count  line max count: the max zero num of one line, default is 50


# Tips #
1. if the source file is huge, suggest you to process the file to min result first.
e.g: histogram_cal -f input.file -n 1 > output.file 
2. if the source file is small, you can process with pip operation, like this,
e.g: cat input.file | histogram_cal -n 10 | histogram_show



