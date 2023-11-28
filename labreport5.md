# Warren Li - CSE 15L Lab Report 5
## Part 1
1. Post from the student:
I am running into a bug with my `merge` function. This is the output from the test cases:
```
JUnit version 4.13.2
.E.
Time: 0.011
There was 1 failure:
1) testMerge1(ListExamplesTests)
array lengths differed, expected.length=4 actual.length=2; arrays first differed at element [2]; expected:<x> but was:<end of array>
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:89)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:28)
        at org.junit.Assert.internalArrayEquals(Assert.java:534)
        at org.junit.Assert.assertArrayEquals(Assert.java:285)
        at org.junit.Assert.assertArrayEquals(Assert.java:300)
        at ListExamplesTests.testMerge1(ListExamplesTests.java:12)
        ... 9 trimmed
Caused by: java.lang.AssertionError: expected:<x> but was:<end of array>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:87)
        ... 15 more

FAILURES!!!
Tests run: 2,  Failures: 1
```

2. TA: In order to debug this issue, I recommend printing and comparing the output from the function. It seems that the cause is that the length of the merged list is different from expected. This likely means that you are leaving out some elements in the input lists.

3. Student: I was able to fix the bug, and my output is below:
```
JUnit version 4.13.2
..
Time: 0.012

OK (2 tests)
```

4. I was using lab7 for this setup.
```
* lab7/
    * lib/
        * hamcrest-core-1.3.jar
        * junit-4.13.2.jar
    * resources/
        * logo.png
        * config.xml
    * ListExamples.java
    * ListExamplesTests.java
    * test.sh
    * .gitignore
```
ListExamples.java:
```
import java.util.ArrayList;
import java.util.List;

interface StringChecker { boolean checkString(String s); }

class ListExamples {

  // Returns a new list that has all the elements of the input list for which
  // the StringChecker returns true, and not the elements that return false, in
  // the same order they appeared in the input list;
  static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(0, s);
      }
    }
    return result;
  }


  // Takes two sorted list of strings (so "a" appears before "b" and so on),
  // and return a new list that has all the strings in both list in sorted order.
  static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while(index1 < list1.size() && index2 < list2.size()) {
      if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
        result.add(list1.get(index1));
        index1 += 1;
      }
      else {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    while(index2 < list2.size()) {
      result.add(list2.get(index2));
      index2 += 1;
      if (index1 < list1.size()) {
        result.add(list1.get(index1));
      }
    }
    return result;
  }


}
```
ListExamplesTests.java:
```
import static org.junit.Assert.*;
import org.junit.*;
import java.util.*;
import java.util.ArrayList;


public class ListExamplesTests {
	@Test(timeout = 500)
	public void testMerge1() {
    		List<String> l1 = new ArrayList<String>(Arrays.asList("x", "y"));
		List<String> l2 = new ArrayList<String>(Arrays.asList("a", "b"));
		assertArrayEquals(new String[]{ "a", "b", "x", "y"}, ListExamples.merge(l1, l2).toArray());
	}
	
	@Test(timeout = 500)
        public void testMerge2() {
		List<String> l1 = new ArrayList<String>(Arrays.asList("a", "b", "c"));
		List<String> l2 = new ArrayList<String>(Arrays.asList("c", "d", "e"));
		assertArrayEquals(new String[]{ "a", "b", "c", "c", "d", "e" }, ListExamples.merge(l1, l2).toArray());
        }

}
```
test.sh:
```
javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests
```


Command line used to run tests:
```
bash test.sh
```
In order to fix the bug, you need to merge the remainder of the two lists correctly by adding a separate while loop to handle list1.

## Part 2
One thing that I learned from my lab experience in the second half of this quarter was how to use Vim. I didn't know how to use Vim to modify files before, and I instead just used VSCode to modify any files. After learning about Vim, I learned this new method of modifying files that can be powerful in certain situations.
