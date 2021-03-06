# Auto-Gradable Exercises

Every mechanic has her favorite screwdrivers, and every good teacher
has different kinds of exercises to check that her students are
actually learning, let them practice their new skills, and keep them
engaged.  Some types of exercise are well known, but others aren't as
widely used as they should be.

The key requirement is that it must be possible to check the answer
automatically. This requirement rules out some useful kinds of
assessment, but many remain.

## Multiple Choice Question

The first type of exercise that works well online is a *multiple
choice question* that presents a question and asks the student to pick
the correct answer from a list.  Doing this might (in fact, should)
require them to do more than just read and remember, and as a previous
post discussed, multiple-choice questions are most effective when
their wrong answers probe for specific misconceptions on the student's
part.

> Example: You are in `/home/marg`.  Use `ls` with an appropriate
> argument to get a listing of the files in the directory
> `/home/marg/seasonal`.  Which of the following files is *not* in
> that directory?
>
> - `autumn.csv`
> - `fall.csv`
> - `spring.csv`
> - `winter.csv`

# Write and Run

The second type of exercise is *write and run*, in which the student
has to write code that produces a specified output. When the code is
submitted, we check its structure and/or output and give feedback.
Write and run exercises can be as simple or as complex as the
instructor wants. For example, it's often enough with novices to
simply ask them to call a function or method: experienced instructors
often forget how hard it can be to figure out which parameters go
where.

> Example: the matrix M contains data read from a file. Using one
> function or method call, create a matrix Z that has the same shape
> as M but contains only zeroes.

Write and run exercises help students practice the skills they most
want to learn, but writing good automated checks is hard: students can
find very creative ways to get the right answer, and it's demoralizing
to give them a false negative.  One way to reduce how often this
occurs is to give them a small test suite they can run their code
against before they submit it (at which point it is run against a more
comprehensive set of tests).  Doing this helps to catch cases in which
students have completely misunderstood the written spec of the
exercise.

To help students realize just how hard it is to write good tests
instructors can get them to do it themselves.  Instead of writing code
that satisfies some specification, they can be asked to write tests to
determine whether a piece of code conforms to a spec.

> Example: the function `monotonic_sum` calculates the sum of each
> section of a list of numbers in which the values are monotonically
> increasing. For example, given the input `[1, 3, 3, 4, 5, 1]`, the
> output should be `[4, 3, 9, 1]`. Write and run unit tests to
> determine which of the following bugs the function contains:
>
> - Considers every negative number the start of a new sub-sequence.
> - Does not include the first value of each sub-sequence in the
>   sub-sum.
> - Does not include the last value of each sub-sequence in the
>   sub-sum.
> - Only re-starts the sum when values decrease rather than fail
>   to increase.

## Fill in the Blanks

*Fill in the blanks* is a refinement of write and run in which the
student is given some starter code and asked to complete it. (In
practice, many write and run exercises are actually fill in the blanks
because the instructor will provide comments to remind the students of
what steps they should take.) Novices often find fill in the blanks
less intimidating than writing all the code from scratch, and since
the instructor has provided most of the answer's structure,
submissions are much easier to check.

> Example: fill in the blanks so that the code below prints the string
> 'hat'.
>
> ```
> text = 'all that it is'
> slice = text[____:____]
> print(slice)
> ```

## Parsons Problem

A *Parsons Problem* is another kind of exercise that avoids the "blank
screen of terror" problem: the student is given the lines of code
needed to solve a problem, but has to put them in the right order.
Research over the past few years has shown that Parsons Problems are
effective because they allow students to concentrate on control flow
separately from vocabulary [[Ericons2017](#ericson-parsons)]. The same
research shows that giving the student more lines than she needs, or
asking her to rearrange some lines and add a few more, makes this kind
of problem significantly harder [[Harms2017](#harms-parsons)].
Parsons Problems can be emulated (albeit somewhat clumsily) by asking
students to rearrange code in an editor.

> Example: rearrange and indent these lines to calculate the sums of the
> positive and negative values in a list.
>
> ```
> positive = 0
> return negative, positive
> if v > 0
> else
> positive += v
> negative = 0
> for v in values
> negative += v
> ```

## Tracing Execution

*Tracing execution* is the inverse of a Parsons Problem: given a few
lines of code, the student has to trace the order in which those lines
are executed. This is an essential debugging skill, and is a good way
to solidify students' understanding of loops, conditionals, and the
evaluation order of function and method calls. Again, we don't yet
support this directly, but it can be emulated by having students type
in a list of line labels.

> Example: in what order are the labelled lines in this block of code
> executed?
>
> ```
> A)     vals = [-1, 0, 1]
> B)     inverse_sum = 0
>        try:
>            for v in vals:
> C)             inverse_sum += 1/v
>        except:
> D)         pass
> ```

## Tracing Values

*Tracing values* is similar to tracing execution, but instead of
spelling out the order in which code is executed, the student is asked
to list the values that one or more variables take on as the program
runs. Again, it can be implemented by having students type in their
answers, but this quickly becomes impractical. In practice, the best
approach is to give the student a table whose columns are labelled
with variable names and whose rows are labelled with line numbers.

> Example: what lines of text pass through the pipes and the final
> redirect when this file:
>
> ```
> 2017-11-01,Akeratu,9
> 2017-11-01,Monona,3
> 2017-11-02,Monona,1
> 2017-11-03,Monona,1
> 2017-11-03,Akeratu,7
> ```
>
> is run through this Unix shell command:
>
> ```
> cut -d , -f 2 filename | sort | uniq > result.txt
> ```

## Minimal Fixes

Returning to debugging skills, another exercise that helps student
develop them is *minimal fixes*. Given a few lines of code that
contain a bug, the student must either make or identify the smallest
change that will produce the correct output. Making the change can be
done as using write and run, while identifying it can be done as a
multiple choice question.

> Example: this function is supposed to test whether a point `(x, y)` lies
> strictly within a rectangle defined by `(x_min, y_min, x_max, y_max)`.
> Change one line to make it do so correctly.
>
> ```
> def inside(point, rect):
>     if (point.x <= rect.x_min): return false
>     if (point.y <= rect.y_min): return false
>     if (point.x >= rect.y_max): return false
>     if (point.y >= rect.y_max): return false
>     return true
> ```

## Small Variations

*Small variation* exercises are similar, but instead of making a
change to fix a bug, the student is asked to make a small alteration
that changes the output in some specific way. These alterations can
include:

-   replacing one function call with another
-   changing one variable's initial value
-   swapping an inner and outer loop
-   changing the order of tests in a chain of conditionals
-   changing the nesting of function calls or the order in which methods
    are chained

Again, this gives students a chance to practice a useful real-world
skill: the fastest way to produce a working program is often to tweak
one that already does something useful.

> Example: change the inner loop control in the function below so that
> it sets the upper left triangle of the matrix to zero.
>
> ```
> def zeroTriangle(matrix):
>     for c in range(matrix.cols):
>         for r in range(matrix.rows):
>             matrix[r, c] = 0
> ```

## Matching

Matching problems are another entire family of exercises.  *One-to-one
matching* gives the student two lists of equal length and asks her to
pair corresponding items, e.g., "match each piece of code with the
output it produces".

> Example: match each function's name with the operation it implements.
>
> | Function | Operation |
> | -------- | --------- |
> | SGEMV    | triangular banded matrix-vector multiply |
> | STBMV    | solve triangular matrix with multiple right-hand sides |
> | STRSM    | matrix-vector multiply |

*Many-to-many matching* is similar, but the lists aren't the same
length, so some items may be matched to several others. Both kinds
require students to use higher-order thinking skills, but many-to-many
are more difficult because students can't do easy matches first to
reduce their search space.  (In technical terms, there is a higher
[cognitive load](load.html).)

Matching problems can be emulated by having students submit lists of
pairs as text (such as "A3, B1, C2"), but that's clumsy and
error-prone. If available, the machinery built for Parsons Problems
can be used let students drag and drop blocks of text to form matches.

## Labelling Diagrams

Drag-and-drop opens many other doors: for example, tracing execution
is easy to implement this way. So is *labelling diagrams*: rather than
students typing in the labels, it is faster and more reliable for them
to drag labels around to attach to the correct elements. The picture
can be a complex data structure ("after this code is executed, which
variables point to which parts of this structure?"), the graph that a
program produces ("match each of these pieces of code with the part of
the graph it generated"), the code itself ("match each term to an
example of that program element"), or many other things.

> Example: label the following diagram to show which structures the
> variables `x`, `y`, and `z` refer to after these three lines of code
> are executed.
>
> ```
> x = 3
> y = [x, x]
> z = [x, y]
> ```
>
> ![Labelling](fig/label.png)

## Drawing Diagrams

*Drawing diagrams* of things like data structures is also
straightforward to do on paper but very difficult to grade
automatically. One way to make solutions gradable may be to constrain
the drawing in the same way that Parsons Problems constrain code
construction, i.e., give students the pieces of the diagram and ask
them to arrange them correctly, but this is a long way off.

## Summarization

We mentioned earlier that matching problems require students to use
higher-order thinking skills. *Summarization* also does this, and
gives them a chance to practice a skill that is very useful when
*reporting* bugs rather than fixing them. For example, students can be
asked, "Which sentence best describes how the output of f changes as x
varies from 0 to 10?" and then given several options as a multiple
choice question. Similarly, ranking problems present the student with
several choices and ask them to order them from fastest to slowest,
most robust to most brittle, and so on. (Ranking is more manageable
when implemented with drag and drop than as a multiple choice
question.)

## Fault Mapping

One other kind of exercise that can be implemented as a multiple
choice question is *fault mapping*: given a piece of buggy code and an
error message, the student has to identify the line on which the error
occurred. In simple cases this will be the line mentioned in the error
message, but in more subtle cases, the student will have to trace
execution forward and backward to figure out where things first went
wrong.

## Others

Other kinds of exercises are hard for any automated platform to
provide.  *Refactoring exercises* are the complement of small
variation exercises: given a working piece of code, the student has to
modify it in some way *without* changing its output. For example, the
student could be asked to replace loops with vectorized expressions,
to simplify the condition in a while loop, etc. The challenge here is
that there are often so many ways to refactor a piece of code that
grading requires human intervention.

> Example: write a single list comprehension that has the same effect
> as this loop.
>
> ```
> result = []
> for v in values:
>     if len(v) > threshold:
>         result.append(v)
> ```

*Code review* is hard to grade automatically in the general case, but
can be tackled if the student is given a rubric (i.e., a list of
faults to look for) and asked to match particular comments against
particular lines of code. For example, the student can be told that
there are two indentation errors and one bad variable name, and asked
to point them out; if she is more advanced, she could be given half a
dozen kinds of remarks she could make about the code without guidance
as to how many of each she should find.  As with tracing values, this
is easiest for students to do when presented as a table, which we
currently don't support.

> Example: using the rubric provided, mark each line of the code below.
>
> ```
> 01)  def addem(f):
> 02)      x1 = open(f).readlines()
> 03)      x2 = [x for x in x1 if x.strip()]
> 04)      changes = 0
> 05)      for v in x2:
> 06)          print('total', total)
> 07)          tot = tot + int(v)
> 08)      print('total')
> ```
>
> 1. poor variable name
> 2. unused variable
> 3. use of undefined variable
> 4. missing values
> 5. fossil code

## Discussion

All of this discussion has assumed that grading must be fully
automatic in order to scale to large classes, but that is not
necessarily true.  [[Paré2008](#pare-joordens-peer)] and
[[Kulkarni2013](#kulkarni-peer-grading)] report experiments in which
learners grade each other's work, and the grades they assign are then
compared with grades given by graduate-level teaching assistants or
other experts.  Both found that student-assigned grades agreed with
expert-assigned grades as often as the experts' grades agreed with
each other, and that a few simple steps (such as filtering out
obviously unconsidered responses or structuring rubrics) decreased
disagreement even further.  Much more research needs to be done, but
given that critical reading is an effective way to learn, this result
may point to a future in which learners use technology to make
judgments, rather than being judged by technology.

## Bibliography

*   <span id="ericson-parsons">[Ericson2017]</span>
    Barbara J. Ericson, Lauren E. Margulieux, and Jochen Rick:
    "Solving Parsons Problems Versus Fixing and Writing Code."
    *Proc. Koli Calling 2017*, November 2017, 10.1145/3141880.3141895.

*   <span id="harms-parsons">[Harms2016]</span>
    Kyle James Harms, Jason Chen, and Caitlin L. Kelleher:
    "Distractors in Parsons Problems Decrease Learning Efficiency for
    Young Novice Programmers."  *Proc. ICER 2016*, September 2016,
    10.1145/2960310.2960314.

*   <span id="kulkarni-peer-grading">[Kulkarni2013]</span>
    Chinmay Kulkarni, Koh Pang Wei, Huy Le, Daniel Chia, Kathryn
    Papadopoulos, Justin Cheng, Daphne Koller, and Scott R. Klemmer:
    "Peer and Self Assessment in Massive Online Classes". *ACM
    Transactions on Computer-Human Interaction*, 20(6), 2013,
    10.1145/2505057.

*   <span id="pare-joordens-peer">[Paré2008]</span>
    D.E. Paré and S. Joordens: "Peering Into Large Lectures: Examining
    Peer and Expert Mark Agreement Using peerScholar, an Online Peer
    Assessment Tool."  *Journal of Computer Assisted Learning*, August
    2008, 10.1111/j.1365-2729.2008.00290.x.
