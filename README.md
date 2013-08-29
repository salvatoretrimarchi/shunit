The shunit script
======

shunit is a bash script for running tests scripts that are written with the shunit library. To use it, fir install it:

    make install

... then run it with the name of a single bash test script or a whole directory of scripts:

    shunit -t test_script.sh
    shunit -t test_directory/

... The default output format is junit. You can select tunit with the '-f' flag:

    shunit -t test_script.sh -f tunit


The shunit library
======

shunit is just a set of bash functions for producing unit test output from bash scripts. I wrote this library because I often found myself writing things in bash whose output I wanted to consume as discrete pass/fail tasks into Bamboo, so I wrote the junit functions. Then later on, I got sick and tired of (as a human) reading junit output, so I wrote the tunit functions, so my scripts could output tunit or junit depending on which flags I passed.

Complete documentation is inside the functions (each function has --help) in ./lib/*unit.sh. A pair of complete examples are in tests/*unit.sh.

Example output
==============

    akesterson@akesterson-pc ~/source/upstream/git/shunit
    $ bash tests/tunit.sh
    [super::class] someTest .... [OK]
    [super::class] someOtherTest .... [FAILED]
	    generic failure : Yo dawg, I heard you like failures
	    This is some raw data, please read it

    ==== 2 TESTS in 0 SECONDS : 1 ERRORS, 1 FAILURES ====

    akesterson@akesterson-pc ~/source/upstream/git/shunit
    $ bash tests/junit.sh
    <?xml version="1.0" encoding="UTF-8"?>
    <testsuite failures="1" time="0" timestamp="Wed Dec 19 22:51:02 EST 2012" errors="1" tests="2">
	<properties/>
	<testcase classname="super::class" time="31337" name="someTest">
	</testcase>
	<testcase classname="super::class" time="31337" name="someOtherTest">
	    <failure type="generic failure" message="Yo dawg, I heard you like failures">
		<![CDATA[
    This is some raw data, please read it
		]]>
	    </failure>
	</testcase>
    </testsuite>
