A copy of RST parser 2.01 http://www.cs.toronto.edu/~weifeng/software.html

- no changes made
- see README.txt

## Installation guides

Tested on Ubuntu 14.04 LTS

### liblbfgs

* Install liblbfgs dev files
* Check your distribution (this one is Ubuntu 14.04)
  
         $apt-cache search liblbfgs
         [...]
         Filename: pool/universe/libl/liblbfgs/liblbfgs0_1.10-5_amd64.deb
         [...]
* Install
  
         $sudo apt-get install liblbfgs-dev

### Build crfsuite-0.12

         $cd feng-hirst-rst-parser-acl-2014-master/tools/crfsuite/crfsuite-0.12/
         $chmod +x configure
         $./configure
* you need to have gcc installed, e.g. `sudo apt-get install build-essential`

         $make
         $sudo make install

* make links to the shared libraries (otherwise crfsuite will fail with `crfsuite: error while loading shared libraries: libcrfsuite-0.12.so: cannot open shared object file: No such file or directory`)
         
         $sudo ln -s /usr/local/lib/libcrfsuite-0.12.so /usr/lib/libcrfsuite-0.12.so
         $sudo ln -s /usr/local/lib/libcqdb-0.12.so /usr/lib/libcqdb-0.12.so
         $sudo ln -s /usr/local/bin/crfsuite /usr/bin/crfsuite-stdin

* check if the installation works:

        $crfsuite-stdin tag -pi -m \ 
        feng-hirst-rst-parser-acl-2014-master/model/tree_build_set_CRF/label/intra.crfsuite \ 
        feng-hirst-rst-parser-acl-2014-master/tools/crfsuite/test.txt
         
        [..]
        @probability	0.003844
        LEAF:0.063117
        Elaboration[N][S]:0.942829
        LEAF:0.060640

### Install python NLTK 2.09b

        $apt-cache show python-nltk

        [..]
        Version: 2.0~b9-0ubuntu4 (on ubuntu 14.04)
        [..]

        $sudo apt-get install python-nltk

### Test if it works

        $feng-hirst-rst-parser-acl-2014-master/src$ python parse.py -t test ../texts/wsj_0607.out
