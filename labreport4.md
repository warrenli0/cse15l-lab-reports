# Warren Li - CSE 15L Lab Report 4

`ctrl + f` `up 6 times` `o` `up` `right 6 times` `<backspace>` `2` `<esc>` `:wq`

4. Log into ieng6
`ssh cs15lfa23pm@ieng6.ucsd.edu <enter>`
<img width="762" alt="Screen Shot 2023-11-13 at 11 04 12 AM" src="https://github.com/warrenli0/cse15l-lab-reports/assets/89435196/e09f4e1c-20d1-4812-9f3f-59dc254ea241">

5. Clone your fork of the repository from your Github account
`git clone git@github.com:warrenli0/lab7.git <enter>`
<img width="566" alt="Screen Shot 2023-11-13 at 11 03 45 AM" src="https://github.com/warrenli0/cse15l-lab-reports/assets/89435196/06bf0c20-fe08-420e-93a8-0c96b635ec57">

6. Run the tests, demonstrating that they fail
`cd lab7 <enter>`
`javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java <enter>`
`java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests <enter>`
<img width="966" alt="Screen Shot 2023-11-13 at 11 06 44 AM" src="https://github.com/warrenli0/cse15l-lab-reports/assets/89435196/c7dbb506-bdd0-428c-a84e-91f3c9e6d7a4">

8. Edit the code file to fix the failing test
`vim ListExamples.java <enter>`
`ctrl + f` `up 6 times` `o` `up` `right 6 times` `<backspace>` `2` `<esc>` `:wq` `<enter>`
<img width="591" alt="Screen Shot 2023-11-13 at 11 13 18 AM" src="https://github.com/warrenli0/cse15l-lab-reports/assets/89435196/38667199-f3b6-428f-992a-2fdbfe8b305e">
<img width="590" alt="Screen Shot 2023-11-13 at 11 16 33 AM" src="https://github.com/warrenli0/cse15l-lab-reports/assets/89435196/2ad8c084-2db1-4f15-9bf4-5ba687d98bdd">

9. Run the tests, demonstrating that they now succeed
`javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java <enter>`
`java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests <enter>`
<img width="981" alt="Screen Shot 2023-11-13 at 11 16 51 AM" src="https://github.com/warrenli0/cse15l-lab-reports/assets/89435196/95f4ad0c-5b89-4e82-a299-24510fa5f10c">

10. Commit and push the resulting change to your Github account
`git add . <enter>`
`git commit -m "Fix ListExamples.java" <enter>`
`git push <enter>`
<img width="724" alt="Screen Shot 2023-11-13 at 11 26 18 AM" src="https://github.com/warrenli0/cse15l-lab-reports/assets/89435196/0eaea40d-11c2-4bda-9e62-15e5dd898122">
