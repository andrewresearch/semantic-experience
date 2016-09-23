#Semantic Experience and System Architecture

[TOC]

##Learning Task with Multiple Learners

### The problem

Consider a learning scenario where we have one student who is required to learn one thing. The student needs to acquire whatever knowledge and/or skills (epistemic resources) necessary to be successful in the learning task (i.e. reach an epistemic target).

However, the student also brings with them an existing context of experience and a pre-existing set of epistemic resources.

### Typical teacher approach

Typically, teachers approach this problem by assessing where the student is at (what are their existing epsitemic resources), identifying the gap between these and what is necessary for the learning task, and crafting a learning experience that is designed to grow the student's epistemic resources to include those that are required for the task. The focus is on a meaningful experience for the student - that is enabling the student to make sense of the task in such a way that they are successful at achieving it.

In a situation where there are multiple students, each with their own experiences and epistemic resources, this becomes a challenging task for the teacher. There is a potential need for multiple semantic experiences that both accommodate the differences between the learners and yet the need to be successful in the same task. 

##Computational Approach A (Traditional)

Learning Analytics requires us to address how the learning scenario above might be addressed computationally. I suggest that the approach that is commonly adopted is as follows.

### Experience context and epistemic target 

Consider a learning task visualised as a context of all possible experiences, and an epistemic target - the desired learning outcome of the task.

![](./ec-1.pdf)

### Learners' epistemic resources

A learner brings their own set of epistemic resources to the task. Many learners come from any different experiences and therefore bring epistemic resources that are not unified in their proximity to the target.

While some learners will have a close alignment of their epistemic resources to the target, others will have almost no alignment.

The learners also approach the target from different directions as they're resources have been developed over time from different experiences.

![](./ec-2.pdf)

### Groups of learners

For any one learning task, a good teacher can identify different kinds of learners. There may be those that quickly pick up new contexts, and those that need time in order to understand. There may be those that learn well collaboratively, and those that prefer to study alone. 

The teacher tends to identify groups that when targeted with a particular type of learning experience are likely to respond positively. Thus, the learning experience may be modified to suit the differences between different groups of students.

This is conceptualised with the grouping of epistemic resources into identifiable clusters. The process of modfiying the experience to suit these groups is akin to moving the clusters closer to the epistemic target in the centre.


![](./ec-3.pdf)

### Quantifying the process

Typically, in systemising learning we attempt to quantify the learning process in some way. For example, how far do these groups need to move to reach the target.

This is conceptualised by breaking the experience space into 16 smaller squares. If we wanted to be more accurate would divide it into 100 squares, or some other arbitrary large number until we achieved the level of desired precision.

![](./ec-4.pdf)

### Identifying the moves

Once we have quantified the space, we can identify the necessary moves to shift each cluster of epistemic resources towards the target. Just as the teacher modifies learning experiences to suit the different groups of learners, we can quantify the necessary differences between the groups with different paths towards the centre.

![](./ec-5.pdf)

### Encoding the moves as rules

Once we've identify the moves, we can encode them as rules. For example, the rule for one group might be to move down 1.5 squares and to the right 1.5 squares, while another group might need to move right 0.5 squares and up 1 square.

In a particular learning task the up/down and left/right shifts may represent the kinds of changes in their knowledge required by the learners. For example, writing more expressively vs more succintly and more reflectively vs more analytically.

Whatever the type of changes that are required, we can represent them by these rules. This enables a systemic approach to capture change in a formalised way.

![](./ec-6.pdf)

### Moving towards the target

The intended outcome is that the learners' epistemic resources become closer to the target over time, representing success in the learning task.

However, the originally identified groups missed some learners which were not caught by the set of rules. We can capture these by creating more groups and/or more rules until the learning task is successful for all cases.

![](./ec-7.pdf)

### Key limitations for the traditional approach

Although the above strategy generally works well for a teacher in a classroom, it has some significant limitations:

1. The experience space in reality is much more complex that the two dimensional example given here
2. The learners' epistemic resources are not static, but are continually changing. Even the learning task itself will affect the learners state in different ways. In other words, the black dots are not in known positions.
3. There may be an unknown number of learners, and therefore an unknown number of clusters of resources. Even if the number of learners is known, because of 2 the clusters are not necessarily predicable.
4. There is no certainty in how the experience should be quantified nor the level of precision required from the quantification.
5. In order catch all possible conditions, the resulting set of rules is likely to be unbounded. Even where it could be bounded, taking a high dimensional space (unlike this trivial example) with a large number of learners that a dynamically changing, is going to result in a rule set that approaches infinity as the system increases in complexity. The approach is therefore not scalable as it can quickly become intractable.

### A new approach is required

Clearly, to address the scenario outlined above, we need a different approach. One that accommodates the unknowns and the dynamism of the learners' epistemic resources.

Ideally, we would like a computational approach that remains the same despite the changes in the data. So rather than creating and modifying rules to accommodate differences, the ability to deal with these differences is built into the computational algorithm itself.

This can be done, but it requires a shift in thinking, and a change in the kind of computational resources to accommodate that thinking.

##Computational Approach B (Alternate)

I'm suggesting that an alternate approach can be taken to addressing the learning task problem computationally, and that this alternate approach addresses the limitations with the traditional approach.

### Representing change rather than state

Rather than quantifying the experience space of the learning task, and assessing where the learners' are likely to be grouped in this space, consider the idea of quantifying the path between the target and the learner.

![](./ec-8.pdf)

### A functional view

At first this appears to be very similar to the previous approach. However, because we are quantifying change between the learner and target, we can represent this differently. We can represent this change as a vector \\(\vec{LT}\\) that is the difference between the learner \\(\vec{L}\\) and the target \\(\vec{T}\\). 

![](./ec-9.pdf)

This can be represented functionally:

\\[  f(\vec{L}) = -\vec{L} + \vec{T} \\]

With this view, irrespective of where the learner is in the experience space, the function for the move to the target is always the same. Adding more learners does not result in any more rules.

The functional view also allows for changes in dimensional complexity without changing the underlying algorithm. For example, in the simple example we are considering the learners' epistemic resources and the target to be 2 dimensional, and so calculating \\(\vec{LT}\\) would look like this:

\\[ \vec{LT} = - \begin{bmatrix} 
x_l \\
y_l 
\end{bmatrix}
+ \begin{bmatrix} 
x_t \\
y_t 
\end{bmatrix} \\]

However, the algorithm is agnostic to dimensionality:

\\[ \vec{LT} = - \begin{bmatrix} 
x_l \\
y_l \\
\vdots \\
n_l
\end{bmatrix}
+ \begin{bmatrix} 
x_t \\
y_t \\
\vdots \\
n_l
\end{bmatrix} \\]

##Architecture change

Addressing the limitations of the first approach required a different way of thinking about the problem. Instead of focussing on where the learners' were at, the problem was reconceived in terms of where they should be headed. While there are conceptual similarities between the two approaches, the way that they might be instantiated in software is likely to be very different. The implementation of approach B requires a very different architecture than approach A.

### Traditional approach architecture

### Alternate approach architecture




