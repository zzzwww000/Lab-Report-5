# LAB REPORT 5
**_By Zichen Wang_**

This Lab Report illustrates the updated and enhanced version on **the script about grading**.
> Thus, this report is based on report 6 - about the editting and updating bash scripts.

## The Required Bash Script
```
CPATH='.:../lib/hamcrest-core-1.3.jar:../lib/junit-4.13.2.jar'

# clone the repository of the student submission
rm -rf submissions
rm -rf tests
git clone $1 submissions
echo 'Finished cloning'

# check the student code has the correct file(s) submitted.
if [ ! -f ./submissions/ListExamples.java ]; then
    echo "You might have the wrong file submitted, please do check again!"
    exit 1
fi

# Copy the student submission out of the submissions folder, and put it to the tests folder
mkdir ./tests
cp ./submissions/ListExamples.java ./tests
cp ./TestListExamples.java ./tests

cd tests
# Compile the student's code and test files
javac -cp $CPATH *.java

# Check if compilation succeeded
if [ $? -ne 0 ]; then
    echo "Error: Compilation failed"
    exit 1
else 
    echo "Compilation Done!"
fi

# Run the tests using JUnit and report the grade

java -cp $CPATH org.junit.runner.JUnitCore TestListExamples > tests_results.txt
grep -o "FAILURES" tests_results.txt > grep_result.txt
if [ -s grep_result.txt ]; then
    echo "Sorry, you failed the tests."
    cat tests_results.txt
else
    echo "Congrats, well done!"
    cat tests_results.txt
fi

exit 0
```

## The Tests provided for running
>Based on week 6 lab page, following tests are required for my `grade.sh` script:

1) https://github.com/ucsd-cse15l-f22/list-methods-lab3, which has the same code as the starter from lab 3

2) https://github.com/ucsd-cse15l-f22/list-methods-corrected, which has the methods corrected (I would expect this to get full or near-to-full credit)

3) https://github.com/ucsd-cse15l-f22/list-methods-compile-error, which has a syntax error of a missing semicolon. Note that your job is not to fix this, but to decide what to do in your grader with such a submission!

4) https://github.com/ucsd-cse15l-f22/list-methods-signature, which has the types for the arguments of filter in the wrong order, so it doesn’t match the expected behavior.

5) https://github.com/ucsd-cse15l-f22/list-methods-filename, which has a great implementation saved in a file with the wrong name.

6) https://github.com/ucsd-cse15l-f22/list-methods-nested, which has a great implementation saved in a nested directory called pa1.

7) https://github.com/ucsd-cse15l-f22/list-examples-subtle, which has more subtle bugs (hints: see assertSame, which compares with == rather than .equals(), and think hard about duplicates for merge)

## General Workflow:
> Since the SSH key gen has been provided for my personal computer that I am working on, the process for logging in will be ignored.

1. Based on reviews and assitance form classmates and Tutors, I have adjusted my codes and finished the remaining of the scripts.
2. It is always possible to remove unnecessary outputs from my terminal by removing `echo` from my script, but for clarification I maintained those stuff.
3. To make sure it works on all files, I used all the 7 tests provided in the lab page.

## Results of tests:

**1. list-methods-lab3, which should fail the test**
```
bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-lab3.git
Cloning into 'submissions'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.
Finished cloning
Compilation Done!
Sorry, you failed the tests.
JUnit version 4.13.2
.E
Time: 0.642
There was 1 failure:
1) testMergeRightEnd(TestListExamples)
org.junit.runners.model.TestTimedOutException: test timed out after 500 milliseconds
        at java.util.Arrays.copyOf(Arrays.java:3210)
        at java.util.Arrays.copyOf(Arrays.java:3181)
        at java.util.ArrayList.grow(ArrayList.java:267)
        at java.util.ArrayList.ensureExplicitCapacity(ArrayList.java:241)
        at java.util.ArrayList.ensureCapacityInternal(ArrayList.java:233)
        at java.util.ArrayList.add(ArrayList.java:464)
        at ListExamples.merge(ListExamples.java:42)
        at TestListExamples.testMergeRightEnd(TestListExamples.java:17)

FAILURES!!!
Tests run: 1,  Failures: 1
```

**2. list-methods-corrected, which should pass the test**
```
bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-corrected.git
Cloning into 'submissions'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.
Finished cloning
Compilation Done!
Congrats, well done!
JUnit version 4.13.2
.
Time: 0.015

OK (1 test)
```

**3. list-methods-compile-error, which should run into an error**
```
bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-compile-error.git
Cloning into 'submissions'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.
Finished cloning
ListExamples.java:15: error: ';' expected
        result.add(0, s)
                        ^
1 error
Error: Compilation failed
```
**4. list-methods-signature, which should pass the test**
```
bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-signature.git
Cloning into 'submissions'...
remote: Enumerating objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 3
Receiving objects: 100% (3/3), done.
Finished cloning
Compilation Done!
Congrats, well done!
JUnit version 4.13.2
.
Time: 0.015

OK (1 test)

```

**5. list-methods-filename, which has the wrong filename so it will not run anyway**
```
bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-filename.git 
Cloning into 'submissions'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.
Finished cloning
You might have the wrong file submitted, please do check again!
```

**6. list-methods-nested, which is nested directory called pa1, so normally it will not compile**
```
bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-nested.git  
Cloning into 'submissions'...
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 4 (delta 0), reused 4 (delta 0), pack-reused 0
Receiving objects: 100% (4/4), done.
Finished cloning
You might have the wrong file submitted, please do check again!
```

**7. list-examples-subtle, which which has more subtle bugs, so should fail the tests**
```
bash grade.sh https://github.com/ucsd-cse15l-f22/list-examples-subtle.git
Cloning into 'submissions'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.
Finished cloning
Compilation Done!
Sorry, you failed the tests.
JUnit version 4.13.2
.E
Time: 0.015
There was 1 failure:
1) testMergeRightEnd(TestListExamples)
java.lang.AssertionError: expected:<[a, a, b, c, d]> but was:<[a, b, c, d]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at TestListExamples.testMergeRightEnd(TestListExamples.java:19)

FAILURES!!!
Tests run: 1,  Failures: 1
```

> **Thus, from the tests, we can see this scripts will catch and detect all errors and provide sufficient output for different assignments.**
