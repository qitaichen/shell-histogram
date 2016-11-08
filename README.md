# Feature #
* to calculate the count result of a datetime file 
* to calculate the diff result of two histogram
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


# Histogram diff # 
to calculate the diff between two histogram
algorithm : sqrt (sum((x/totalx-y/totaly)^2)/n)
x: the val count of first histogram
y: the val count of standard hisgogram
totalx: the total count of first histogram
totaly: the total count of standard histogram
n: the total timeBlock size 

e.g: 
first file 

    2016-01-01 12:01:00,10
    2016-01-01 12:02:00,11
    2016-01-01 12:03:00,12

standard file 

    2016-01-01 12:01:00,15
    2016-01-01 12:02:00,10
    2016-01-01 12:03:00,12
    

calculate detail : 

    totalx = 10+11+12 = 33
    totaly = 15+10+12 = 37
    result
        = sqrt ( ((10/33-15/37)^2 + (11/33-10/37)^2 + (12/33-12/37)^2 ) / 3)
        = sqrt ( ( 0.010480662 + 0.00397695 + 0.001545436) / 3) 
        = sqrt ( .005334349 ) 
        = 0.0730366


# Tips #
1. if the source file is huge, suggest you to process the file to min result first.
e.g: histogram_cal -f input.file -n 1 > output.file 
2. if the source file is small, you can process with pip operation, like this,
e.g: cat input.file | histogram_cal -n 10 | histogram_show
3. the time block should be format as %Y-%m-%d %H:%M:%s


