# Warren Li - CSE 15L Lab Report 3
## Part 1:
Bug for the `reversed` function in the `ArrayExamples` class in `ArrayExamples.java`.
```
// Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
```
Failure inducing input:
```
@Test
  public void testReversed() {
    int[] input2 = { 1, 2, 3 };
    assertArrayEquals(new int[]{ 3, 2, 1 }, ArrayExamples.reversed(input2));
  }
```
Input that doesn't induce a failure:
```
@Test
  public void testReversedPass() {
    int[] input1 = { };
    assertArrayEquals(new int[]{ }, ArrayExamples.reversed(input1));
  }
```
Symptom: <br/>
<img width="700" alt="Screen Shot 2023-11-03 at 4 53 12 PM" src="https://github.com/warrenli0/cse15l-lab-reports/assets/89435196/a072400a-fb02-4920-801a-4585b01ed3e1"><br/>
The Bug:
Before:
```
// Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
```
After:
```
// Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      newArray[i] = arr[arr.length - i - 1];
    }
    return newArray;
  }
```
I changed the assignment in the for loop to write values into the `newArray` from `arr` rather than into `arr` from `newArray`. Then I would return `newArray` at the end. This fixes the bug because before, it was writing from `newArray` to `arr`. `newArray` was just an empty list so it would just overwrite `arr` as an empty list, which would be returned. By switching the direction of assignment, the bug is fixed.

## Part 2:
I will be finding uses for the `grep` command.
1. Basic file search
   - `grep "10:" technical/911report/chapter-1.txt`
     Output:
     ```
     In response, Jarrah immediately began to roll the airplane to the left and right, attempting to knock the passengers off balance. At 9:58:57, Jarrah told another hijacker in the cockpit to block the door. Jarrah continued to roll the airplane sharply left and right, but the assault continued. At 9:59:52, Jarrah changed tactics and pitched the nose of the airplane up and down to disrupt the assault. The recorder captured the sounds of loud thumps, crashes, shouts, and breaking glasses and plates. At 10:00:03, Jarrah stabilized the airplane.
     ...
     ```
    This command will find all the timestamps with "10:" in it, which will allow you to find events during specific times.
   - `grep " war " technical/911report/chapter-1.txt`
     Output:
     ```
     The President's motorcade departed at 9:35, and arrived at the airport between 9:42 and 9:45. During the ride the President learned about the attack on the Pentagon. He boarded the aircraft, asked the Secret Service about the safety of his family, and called the Vice President. According to notes of the call, at about 9:45 the President told the Vice President:"Sounds like we have a minor war going on here, I heard about the Pentagon. We're at war . . . somebody's going to pay."
     ```
   This command will find all the lines with occurences of the search term. This is useful if you are trying to find where some keywords are used in a document.
3. Case insensitive search
   - `grep -i " WaR " technical/911report/chapter-1.txt`
     Output:
     ```
     The threat of Soviet bombers diminished significantly as the Cold War ended, and the number of NORAD alert sites was reduced from its Cold War high of 26. Some within the Pentagon argued in the 1990s that the alert sites should be eliminated entirely. In an effort to preserve their mission, members of the air defense community advocated the importance of air sovereignty against emerging "asymmetric threats" to the United States: drug smuggling, "non-state and state-sponsored terrorists," and the proliferation of weapons of mass destruction and ballistic missile technology.
     The President's motorcade departed at 9:35, and arrived at the airport between 9:42 and 9:45. During the ride the President learned about the attack on the Pentagon. He boarded the aircraft, asked the Secret Service about the safety of his family, and called the Vice President. According to notes of the call, at about 9:45 the President told the Vice President:"Sounds like we have a minor war going on here, I heard about the Pentagon. We're at war . . . somebody's going to pay."
     ```
   This command allows you to find all occurrences of the word "War" without case sensitivity.
   - `grep -i " Pentagon " technical/911report/chapter-1.txt`
     Output:
     ```
     At 9:34, Ronald Reagan Washington National Airport advised the Secret Service of an unknown aircraft heading in the direction of the White House. American 77 was then 5 miles west-southwest of the Pentagon and began a 330-degree turn. At the end of the turn, it was descending through 2,200 feet, pointed toward the Pentagon and downtown Washington. The hijacker pilot then advanced the throttles to maximum power and dove toward the Pentagon.
     ...
     ```
   This command will find all the lines with occurences of the search term, but the `-i` makes it ignore case, which is useful for finding words that are sometimes capitalized but not others.
4. Recursive search
   - `grep -r "magic" technical/`
     Output:
     ```
     technical//government/About_LSC/State_Planning_Special_Report.txt:to the field, there is no "magic number" of legal services programs
     technical//government/Media/CommercialAppealMemphis2.txt:many say has worked magic with little more than gumption,
     technical//plos/journal.pbio.0020394.txt:        nothing inherently special or magical about the brain that allows it to be intelligent,’the
     technical//plos/journal.pbio.0020054.txt:        grasses rubbing together or even by magic. A fire scientist whose doctorate is in tropical
     technical//plos/pmed.0010042.txt:        ‘A partnership between a celebrity and a brand has an intangible sort of magic’, writes
     technical//plos/journal.pbio.0020028.txt:        selectivity of RNAi: like the fabled “magic bullet,” an RNAi sequence seeks out and
     technical//911report/chapter-6.txt:                telling him that they were waiting for the magic words from the CIA and the FBI. Nor
     ```
   The command will find all files that contain the word "magic" which is useful when you are trying to find all files that mnetion a specific topic.
   - `grep -r "fantasy" technical/`
     Output:
     ```
     technical//government/Post_Rate_Comm/Gleiman_gca2000.txt:story, Denton was leaning into the plate in fantasy baseball camp
     ```
   This command will search through all of the files in the directory for the given search term. This is useful for searching a large set of texts.
5. Latex as search term
   - `grep "^[A-Z][A-Z]" technical/911report/chapter-1.txt`
     Output:
     ```
     INSIDE THE FOUR FLIGHTS
     IMPROVISING A HOMELAND DEFENSE
     NORAD Mission and Structure. NORAD is a binational command established in 1958 between the United States and Canada. Its mission was, and is, to defend the airspace of North America and protect the continent. That mission does not distinguish between internal and external threats; but because NORAD was created to counter the Soviet threat, it came to define its job as defending against external attacks.
     FAA Awareness. Although the Boston Center air traffic controller realized at an early stage that there was something wrong with American 11, he did not immediately interpret the plane's failure to respond as a sign that it had been hijacked. At 8:14, when the flight failed to heed his instruction to climb to 35,000 feet, the controller repeatedly tried to raise the flight. He reached out to the pilot on the emergency frequency. Though there was no response, he kept trying to contact the aircraft.
     FAA Awareness. One of the last transmissions from United Airlines Flight 175 is, in retrospect, chilling. By 8:40, controllers at the FAA's New York Center were seeking information on American 11. At approximately 8:42, shortly after entering New York Center's airspace, the pilot of United 175 broke in with the following transmission:
     NATIONAL CRISIS MANAGEMENT
     ```
   Thie command will find all lines in the file that follow the Latex structure, which can be useful for looking up specific features, such as a phone number.
   - `grep "^[0-9]" technical/911report/chapter-1.txt`
     Output: empty
   This command will search through the file for strings that match the given latex, which is interesting. This allows for more complex search patterns.

Source: ChatGPT<br/>
Modifications: I modified the output by taking the 4 ways that I can use `grep` and running them on the local directory.<br/>
Prompt: What are 4 different ways that I can use `grep` in command-line<br/>
Output:
`grep` is a powerful command-line tool used in Unix and Unix-like operating systems for searching text using patterns. It can be used in a variety of ways to find specific patterns of text in files, output of other commands, and more. Here are four different ways you can use `grep`:

### 1. Basic Text Search

The most basic use of `grep` is to search for a specific string in a file. For example:

```bash
grep "search term" filename.txt
```

This command will search for the phrase "search term" in `filename.txt` and display all the lines where the phrase is found.

### 2. Case-Insensitive Search

You can perform a case-insensitive search using the `-i` option. This is useful when the case of the text is not known or is mixed.

```bash
grep -i "search term" filename.txt
```

This will find "search term", "Search Term", "SEARCH TERM", etc., in `filename.txt`.

### 3. Recursive Search in Directories

If you want to search for a term in all files under a specific directory (and its subdirectories), you can use the `-r` or `-R` option. This is particularly useful in large projects to find where certain terms or codes are used.

```bash
grep -r "search term" /path/to/directory/
```

This command searches for "search term" in all files located in the specified directory and all its subdirectories.

### 4. Piping with Other Commands

`grep` can be used in combination with other commands through piping (`|`). For example, if you want to check which processes are running for a specific program:

```bash
ps aux | grep "program_name"
```

This command first lists all running processes with `ps aux`, then `grep` filters out lines that contain "program_name".

### Bonus: Using Regular Expressions

`grep` stands for "global regular expression print," and one of its powerful features is the ability to search using regular expressions. This allows for more complex search patterns.

```bash
grep "^[A-Z]" filename.txt
```

This command searches for lines that start with a capital letter in `filename.txt`.

Each of these uses showcases the flexibility and power of `grep` in different scenarios, making it an indispensable tool in text processing and search operations in the command line environment.
