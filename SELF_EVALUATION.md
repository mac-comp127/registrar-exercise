# Take-Home Activity: Registrar, Part 2

## Self-Evaluation Rubric

# Correctness

Use the list below to evaluate the correctness of your solution. Cross off the items that your solution passes.

- [ ] The `GameCharacter` class mentions `Weapon` in four places:


- [ ] You have a `drop()` method implemented so that after a student drops a class:
  - [ ] The course is no longer on the course list of that student.
  - [ ] The student is no longer on the roster for the course.
  - [ ] The student is no longer on the waitlist for the course.
  - [ ] The code ensures that _all_ previous invariants still hold true, including the rule that if a course is not full, its waitlist is empty.
- [ ] Your code ensures that enrollment limits can change by modifying `setEnrollmentLimit()`
  - [ ] You used the code snippet in the README to address rule 1 in the new contract.
  - [ ] You wrote a new method called `enrollFromWaitlist()` to address rule 2 in the new contract.
  - [ ] You removed old tests that are no longer relevant.
- [ ] The Javadoc comments are all up to date:
  - [ ] `drop()` has up-to-date Javadoc.
  - [ ] `setEnrollmentLimit()` has up-to-date Javadoc.
  - [ ] The Javadoc for `getWaitlist()` is updated so that it accurately details how waitlisted students are automatically added after both features are implemented.
- [ ] The tests in `RegistrarTest` all pass.
  - [ ] Yes, I ran them one extra time just to make sure!

# Code Style

Use the list below to evaluate the adherence of your code to the [COMP127 Style Guide](https://comp127.innig.net/resources/style-guide/). Cross off the items that your code satisfies.

- [ ] all classes are in packages
- [ ] package names start with a lowercase letter
- [ ] newly created Java files have a header comment with (a) author name, (b) brief description of class, and (c) acknowledgement, if appropriate
- [ ] identifier (variable and method) names are descriptive
- [ ] **variable** and **method** names are in lowerCamelCase (no CapitalizedNames,  names\_with\_underscores)
- [ ] **class** names are singular nouns
- [ ] **class** names are in UpperCamelCase
- [ ] all instance variables are **private**
- [ ] proper indentation:
  - [ ] opening curly braces (“{”) are at the end of the line
  - [ ] closing curly braces (“}”) are on their own line
  - [ ] the indentation of closing braces is the same as the indentation of the opening statements they match
  - [ ] lines are indented according to how deeply they are nested
- [ ] completed TODO comments are deleted
- [ ] extra blank lines are deleted
- [ ] unneeded commented lines of code are deleted
- [ ] print statements used for testing are deleted

# Reflection

Briefly reflect in writing on your experience solving this exercise. Just a
sentence or two in response to each question is plenty.

1. What did you learn from the style of programming and thinking that this exercise asked you to do? How did it feel to work this way?



2. What do you want to remind yourself about _when_ to use this kind of meticulous thinking in your future programming? Write a short note to your future self:



3. Here are complete and correct implementations of the `setEnrollmentLimit()` method:

    public void setEnrollmentLimit(int limit) {
        if (limit < 0) {
            throw new IllegalArgumentException("course cannot have negative enrollment limit: " + limit);
        }
        if (getRoster().size() > limit) {
            throw new IllegalArgumentException("cannot set limit below class size");
        }

        this.enrollmentLimit = limit;

        enrollFromWaitlist();
    }

  ...and the `drop()` method:

    void drop(Student student) {
        waitlist.remove(student);
        roster.remove(student);
        enrollFromWaitlist();
    }

  ...and `enrollFromWaitlist`:

    private void enrollFromWaitlist() {
        while (!getWaitlist().isEmpty() && getRoster().size() < enrollmentLimit) {
            waitlist.remove(0).enrollIn(this);
        }
    }

  These implementations are just _one_ possibility. What you wrote probably looks different in some way. Compare these solutions to yours. What is something you notice from that comparison that you can learn from?



