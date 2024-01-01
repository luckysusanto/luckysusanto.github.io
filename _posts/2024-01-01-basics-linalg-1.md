---
title: 'Linear Algebra for Machine Learning (Part 1 of 4)'
date: 2199-01-01
permalink: /posts/2024/01/basics-linalg-1
tags:
  - basics
  - maths
  - linear algebra
---

# Overview
The target audience of this blog series are those interested in Machine Learning, but has little or weak understanding on linear algebra. This blog series will cover the basics in linear algebra, spanning over **(1) Basics of Vectors and Matrices and Operating with Them**, **(2) Determinants and Inverse**, **(3) Eigenvalues and Eigenvectors**, **(4) Singular Value Decomposition**. Feel free to skip over sections you are confident in.

This blog post will specifically deal with what vectors and matrices are, what we can do with them, and the intuition behind their structure.

# Vectors and Matrices 
In the field of Machine Learning (ML), **Vectors and Matrices** are commonly used as a tool for representing data. Since machines do not have the same senses as we do, we must convert these data into a representation machines can process, which would be numbers - a lot of them. One neat way to represent these numbers are by using vectors.

## Vectors
>**Simplified Definition:** 
>Vectors are a group of numbers in a given context.

Let's leap forward with an example. Say that you are shopping for items in a super-mini market that only have 3 items which are: Apple, Banana, Milk. You then go to buy 3 Apples and 2 Bananas. In a spreadsheet, that would look like the table below.

| Apple | Banana | Milk |
|:-----:|:------:|:----:|
|   3   |    2   |  0   |

A vector is simply the entry of that spreadsheet: $\begin{pmatrix} 3-Apple & 2-Banana & 0-Milk \end{pmatrix}$

As long as you guarantee that the context never changes (i.e. the first entry always talk about amount of apple bought, the second entry always talk about amount of banana bought, etc), you can remove the context from the vector, so that you only have:
$\begin{pmatrix} 3 & 2 & 0 \end{pmatrix}$

The above vector is called a **horizontal vector**. From the name, you might guess that a **vertical vector** exist, and you'd be right! An equivalent vertical vector would be:
$\begin{bmatrix} 3 \\ 2 \\ 0 \end{bmatrix}$ 
Other than their orientation, they are perfectly identical! For now, you can use any format you want. But, for the remainder of this section, I will be using a horizontal vector.

While the question of "is math discovered or invented" is not yet answered, the concept of **Vector** is definitely a human invention. We use vectors to help us organize multiple numbers in a specific context like the example above. This  means that the following two vectors are identical:  $\begin{pmatrix} 3-Apple & 2-Banana & 0-Milk \end{pmatrix}\\ 
\quad = \quad \\ 
\begin{pmatrix} 2-Banana & 0-Milk & 3-Apple\end{pmatrix}$
While the above two vectors are identical, you can no longer remove the identifier of Apple, Banana, and Milk. Of course, you can still use vectors like this, but it doesn't help us represent numbers with context in a neat way, which defeats the purpose of vectors.

## Operating with Vectors
Despite (or because of) its simplicity, there are multitude of thing you can do with vectors. For now, you only need to understand a few operations, namely:
 1. Addition and Subtraction
 2. Scalar Multiplication
 3. Dot Product
 
 ### 1. Vector Addition and Subtraction
We defined vectors as a group of numbers within a specific context. Hence, addition and subtraction can only be performed for two vectors under the same context. An example of the addition of two vectors under the same context:

$\begin{pmatrix} 3[Apple] & 2[Banana] & 0[Milk] \end{pmatrix} \bm{+} \begin{pmatrix} 3[Apple] & 2[Banana] & 1[Milk] \end{pmatrix} \quad = \quad \begin{pmatrix} 6[Apple] & 4[Banana] & 1[Milk] \end{pmatrix}$

You may argue that we can add two vectors under different contexts like such:
$\begin{pmatrix} 3[Apple] & 2[Banana] & 0[Milk] \end{pmatrix} \bm{+} \begin{pmatrix} 3[Banana] & 2[Orange] \end{pmatrix} \quad = \quad \begin{pmatrix} 3[Apple] & 5[Banana] & & 2[Orange] & 0 [Milk] \end{pmatrix}$
While the addition of these two vectors make sense in a glance, there are many problems with it. For one, confusion arises with where should we put the entry for "Orange". Why didn't we put it in as the **x-th** element instead? Remember, we use vectors to represent numbers with context in a neat way. Allowing the addition or subtraction of two vectors with different contexts are just a hassle we shouldn't care about -- and in it's application, we truly don't. 

Now, if we ensure that all of the vectors in our equations are under the same context, we can remove the additional information and shorten how we perform vector addition, turning the first *way too detailed* example into:

$\begin{pmatrix} 3 & 2 & 0 \end{pmatrix} \bm{+} \begin{pmatrix} 3 & 2 & 1 \end{pmatrix} \quad = \quad \begin{pmatrix} 6 & 4 & 1 \end{pmatrix}$

### Vector and Scalar Multiplication
Sometimes, we also want to add the same vectors together multiple times, I'm sure you can figure out an example for yourself. An illustration of where this would be useful is when you go to the same super-mini market to buy your monthly groceries for over 6 months. If each month you would buy 2 Apples, 0 Bananas, and 2 Milk; How much of each item have you bought in the past 6 months?

> **Formal Definition:**
> $x * \begin{pmatrix} i & j & k \end{pmatrix} = \begin{pmatrix} x*i & x*j & x*k \end{pmatrix}$

Intuitively, our example case can be represented into:
$6[Month]* \begin{pmatrix} 2[Apple/Month] & 0[Banana/Month] & 2[Milk/Month]\ \end{pmatrix} = \begin{pmatrix} 12[Apple] & 0[Banana] & 12[Milk] \end{pmatrix}$

And, if we already know the context of our vectors, we can omit most of the details into:
$6* \begin{pmatrix} 2& 0 & 2 \end{pmatrix} = \begin{pmatrix} 12 & 0 & 12 \end{pmatrix}$

If you paid attention to the example, you will realize that the Scalar and the Vector are no longer in the exact same context. In fact, the context of the scalar, the represented vector, and the resulting vector all have different context now. But, individually, each vector is limited to a given context and **as long as they make sense contextually, scalar multiplication can be used**

### Dot Product
Imagine that you are now the cashier of the super-mini market. When someone come into the store, you want to bill them the correct amount. Let's say an Apple cost 1R, a Banana cost 2R, and a Milk cost 3R. Then, how much should you bill someone that is buying 2 Apples and 3 Bananas?

We can represent this problem into vectors!
$\begin{pmatrix} 2[Apple] & 3[Banana] & 0[Milk] \end{pmatrix} \cdot \begin{pmatrix} 1[R/Apple] & 2[R/Banana] & 3[R/Milk] \end{pmatrix} = 2R+6R=8R$

The $\cdot$ symbol indicates that two vectors are being "dotted". As you can see, we perform an element-wise multiplication using the two **related** contexts of both vectors. When we understand the contexts of both vectors, we can omit the details and obtain:
$\begin{pmatrix} 2 & 3 & 0 \end{pmatrix} \cdot \begin{pmatrix} 1 & 2 & 3 \end{pmatrix} = 2*1+3*2=2+6=8$

You might ask "Why isn't this just called vector multiplication?", the answer is to avoid confusion and enhance clarity. This is because, there are other type of vector multiplication such as "Cross Product", which we will not discuss in this post.

## Matrices
While vectors organizes numbers with context in a neat way, **Matrices** utilizes them to solve problems. Simply put, matrices are a group of vectors. More specifically, matrices consist of either **Horizontal Vectors** or **Vertical Vectors**. The distinction is important because we are working with **context**.

Let's say we have a vector that indicates what a certain customer bought in a super-mini market. Customer **A**sta bought 9 Apples, 8 Bananas, and 7 Milks; **B**althier bought 3 Apples, 0 Banana, and 1 Milk; 

The vector that represent what Asta bought (symbolized as $\vec{A}$) would be $\begin{pmatrix} 9 & 8 & 7 \end{pmatrix}$ or $\begin{bmatrix} 9 \\ 8 \\ 7 \end{bmatrix}$; While the vector that represent what Balthier bought ($\vec{B}$) would be $\begin{pmatrix} 3 & 0 & 1 \end{pmatrix}$ or $\begin{bmatrix} 3 \\ 0 \\ 1 \end{bmatrix}$.

Now, we can create two different matrices, consisting of either horizontal or vertical vectors.

### Matrix with Horizontal and Vertical Vectors
#### With Horizontal Vectors
Matrix consisting of horizontal vectors would look like your standard spreadsheet:
| ID | Apple | Banana | Milk |
|:--:|:-----:|:------:|:----:|
| $\vec{A}$ |   9   |    8   |  7   |
| $\vec{B}$ |   3   |    0   |  1   |
In matrix form, it would look like this:
$\begin{bmatrix} 
  9[Apple] & 8[Banana] & 7[Milk] \\
  3[Apple] & 0[Banana] & 1[Milk]
\end{bmatrix}$

And, when we know the context, we can omit the identifier:
$\begin{bmatrix} 
  9 & 8 & 7 \\
  3 & 0 & 1
\end{bmatrix}$

We call the above matrix as a 2 by 3 matrix (2 columns and 3 rows)

#### With Vertical Vectors
Matrix consisting of vertical vectors would look like this
|  Item  | $\vec{A}$ | $\vec{B}$|
|:------:|:---------:|:--------:|
| Apple  |     9     |      3   |
| Banana |     8     |      0   |
| Milk   |     7     |      1   |

Turning it into a matrix is simply done by omitting the details, creating a 3 by 2 matrix like such:
$\begin{bmatrix} 
9 & 3 \\  
8 & 0  \\
7 & 1
\end{bmatrix}$

#### What They Represent
**Both of these matrices represent the same thing**: Asta bought 9 Apples, 8 Bananas, and 7 Milk; While Balthier bought 3 Apples and 1 Milk. In regards to what they represent, you can even say that both of these matrices are identical. However, the way the contexts are represented is an important difference in many cases, and this all comes from how we define **Matrix Multiplication**.

## Operating with Matrices
Alone, a matrix is no different from a spreadsheet. However, we can obtain a lot of new information by operating with multiple matrices that have related contexts. In this post, we will talk about 3 Operations we can do with matrices:

 1. Addition or Subtraction
 2. Scalar Multiplication
 3. Matrix Multiplication

### 1. Matrix Addition  and Subtraction
Since matrices consist of vectors, the same definition apply when we want to perform addition and subtraction between two matrices: **They must be in identical context**. With an identical context, the addition or subtraction between two matrices become an element-wise addition or subtraction.

To illustrate, say that you are trying to analyze your expenses over the past three months. Each month, you set your Budget ($B$) into two types (For your fundamental needs and entertainment) and categorize your Expense into two outlets ($E$) (Fundamental needs, Entertainment). We can create two matrices, each being a 2 by 3 matrix, creating something like this:
$I = 
\begin{bmatrix} 
(Feb) & (Jan) & (Mar)\\
100R & 125R & 150R \\  
40R & 20R  & 30R
\end{bmatrix}, E = 
\begin{bmatrix}
(Feb) & (Jan) & (Mar)\\ 
80R & 95R & 80R \\  
20R & 40R & 40R
\end{bmatrix}$ 

You can perform subtraction between both of these matrices to get  information on where you are over-spending, obtaining the matrix $T$:
$\begin{bmatrix}
(Feb) & (Jan) & (Mar)\\ 
20R & 30R & 70R \\  
20R & -20R & -10R
\end{bmatrix}$

Again, omitting the information we obtain:
$\begin{bmatrix} 
20 & 30 & 70 \\  
20 & -20 & -10
\end{bmatrix}$

Here, we can see that we are over-spending over our set budget for our Entertainment!

### 2. Matrix and Scalar Multiplication
Identical with Scalar Multiplication on Vector, as long as the context of each matrix's element and the scalar have related context, you simply multiply each matrix's element with the scalar.
> **Formal Definition:**
> $x * \begin{bmatrix} a & b & c\\ i & j & k \end{bmatrix} = \begin{bmatrix} x*a & x*b & x*c\\x*i & x*j & x*k \end{bmatrix}$

### 3. Matrix Multiplication
The last operation, and perhaps the most used matrix operation in Machine Learning, is Matrix Multiplication. Let's start with an illustration of a group of three friends that want to buy the same three type of items in different quantities. Asta wants to buy 9 Apples, 8 Bananas, and 7 Milk; Balthier wants to buy 3 Apples and 1 Milk; and Cindy wants to buy 4 Apples and 2 Bananas. Each of them have the option to visit store X or store Y which has differing prices for some items. Store X priced Apple at 1R each, Banana at 2R each, Milk at 4R each; Meanwhile Store Y prices Apple at 1R each, Banana at 1.5R each, and Milk at 5R each. The question is, which store should each of them go to so that they can buy what they want at smallest price possible?

Let's transform this problem into matrices for now. Our demand matrix ($D$) and store price matrix ($P$) would be:
 $D = 
 \begin{bmatrix} 
 9[apple] & 8[banana] & 7[milk]\\
 3[apple] & 0[banana] & 1[milk]\\
 4[apple] & 2[banana] & 0[milk]  
 \end{bmatrix}, \\
 \quad \\
 P = \begin{bmatrix} 
1[R/apple] & 2[R/banana] & 4[R/milk] \\
1[R/apple] & 1.5[R/banana] & 5[R/milk]
\end{bmatrix}$
We just reduced a paragraph worth of information into two neat-looking matrices! Though we can omit the information, I'll let it be for now. 

Before we talk about matrix multiplication, how would you find which store is the best one for each person? Well, you would calculate the price each person has to pay at each store, totaling into 6 cases all together! Then, how can we solve this problem with matrix multiplication? 

Let's start by defining how we perform matrix multiplication:
> **Simplified Definition:**
> The multiplication between two matrices A and B is conducted by performing dot product on each of A's horizontal vector and each of B's vertical vector 
> **Formal Definition:**
> $\begin{bmatrix}a & b & c \\ d & e & f\end{bmatrix} \cdot \begin{bmatrix} i & j \\ k & l \\m & n\end{bmatrix} = \begin{bmatrix} [a & b & c] \cdot [i & k & m] && [a & b & c] \cdot[j & l & n] \\
[d & e & f] \cdot [i & k & m] && [d & e & f] \cdot[j & l & n]
\end{bmatrix}\\ = \begin{bmatrix} w & x \\ y & z\end{bmatrix}$

Through the definition, some question may arise, such as: "This would only work if the horizontal vectors of the first matrix has the same length as the vertical vectors of the second matrix!", And you'd be right! **Matrix multiplication is only defined when the first matrix has as much columns as the second matrix's row.** In mathematical terms, if the first matrix is an **i by j** matrix then the second matrix must be a **j by k** -- And the resulting matrix will be an **i by k** matrix. Okay, maybe this seems abstract for now, so, let's go back to our example.

As it stands, our $D$ matrix is a 3 by 3 matrix while our $P$ matrix is a 2 by 3 matrix. We can't perform a matrix multiplication of $D \cdot P$ right now! 

 $D = 
 \begin{bmatrix} 
 9[apple] & 8[banana] & 7[milk]\\
 3[apple] & 0[banana] & 1[milk]\\
 4[apple] & 2[banana] & 0[milk]  
 \end{bmatrix}, \\
 \quad \\
 P = \begin{bmatrix} 
1[R/apple] & 2[R/banana] & 4[R/milk] \\
1[R/apple] & 1.5[R/banana] & 5[R/milk]
\end{bmatrix}$

   > **You might be wondering:** 
   > While we can't perform $D \cdot P$, we can perform $P \cdot D$ because their size matches! Well, you are right, $P$ is a 2 by 3 matrix and $D$ is a 3 by 3 matrix and the resulting matrix would be a 2 by 3 matrix as well. However, the context does not match! The horizontal vectors in $P$ contextualize the price of one apple, banana, and milk; While the vertical vectors in $D$ contextualize how much of an item each person wants to buy! The context doesn't make sense! This is the reason why $D \cdot P \neq P \cdot D$ -- It's not the size of matrices that matters, it's the context that each row and columns of each matrices represents that matters.

If you remember on how we define a matrix, you will recall that a matrix can consist of either horizontal vectors or vertical vectors. This information is what we will use to satisfy the condition of matrix multiplication! We will just turn matrix $P$ from a matrix consisting of horizontal vectors into one that consists of vertical vectors! Let's make one right now:
$P^T = \begin{bmatrix} 
1[R/apple] & 1[R/apple] \\
2[R/banana] & 1.5[R/banana] \\
4[R/milk] & 5[R/milk]
\end{bmatrix}$
Why did we add a ($^T$) on $P$? It symbolizes that we have just **Transposed** the matrix P. It's essentially just a fancy way of saying we turned it from a matrix consisting of horizontal vectors into one consisting of vertical vectors -- or vice versa! What would happen if you Transpose the matrix $P^T$ then? I believe you can figure out that yourself!

As you may now realize, each horizontal vector of matrix $D$ now has a related context to each vertical vector of matrix $P^T$. This means that we can now perform the dot product between them -- which mean, we can also perform matrix multiplication!
$D \cdot P^T = \\
\begin{bmatrix}
 9[apple] & 8[banana] & 7[milk]\\
 3[apple] & 0[banana] & 1[milk]\\
 4[apple] & 2[banana] & 0[milk]  
\end{bmatrix} \cdot  
\quad \\ \quad \\
\begin{bmatrix}
1[R/apple] & 1[R/apple] \\
2[R/banana] & 1.5[R/banana] \\
4[R/milk] & 5[R/milk]
\end{bmatrix} = \quad \\ \quad \\
\begin{bmatrix} 
9R + 16R + 28R & 9R + 12R +35R \\ 
3R + 0R + 4R & 3R + 0R + 5R \\
4R + 4R + 0R & 4R + 3R + 0R 
 \end{bmatrix} = \quad \\ \quad \\
 \begin{bmatrix}53R & 56R \\
 7R & 8R \\
 8R & 7R\end{bmatrix}$

Now that we understand the context, we can remove the uneeded information, turning the calculation into:
$D \cdot P^T = \\
\begin{bmatrix}
 9 & 8 & 7\\
 3 & 0 & 1\\
 4 & 2 & 0  
\end{bmatrix} \cdot  
\begin{bmatrix}
1 & 1 \\
2 & 1.5 \\
4 & 5
\end{bmatrix} = 
\begin{bmatrix} 
9+ 16 + 28 & 9 + 12 +35 \\ 
3 + 0 + 4 & 3 + 0 + 5 \\
4 + 4 + 0 & 4 + 3 + 0 
 \end{bmatrix} = \quad \\ \quad \\
 \begin{bmatrix}53 & 56 \\
 7 & 8 \\
 8 & 7\end{bmatrix}$
Now, the resulting matrix, can you figure out the context behind each of the entries? The first row shows how much Asta will be billed on Store X and Store Y; The first column shows how much each person will be billed if they all go to Store X with their current shopping list!

Using matrices to organize our numbers with related contexts neatly, and then using matrix multiplication to obtain information for another contexts -- Of course, you don't have to use matrix to solve this problem. But, you'd be hard pressed to say that this isn't a neater system!

#### Bonus on The History of Matrix Multiplication
You might wonder why matrix multiplication is defined the way it is. The short answer relates to what matrix was used back in the day: To keep numbers in a certain contexts organized **for systems of linear substitution**. Why this system works for that specific problem is answered in [this post](https://math.stackexchange.com/questions/271927/why-historically-do-we-multiply-matrices-as-we-do). Anyway, even to this day, we still use matrix multiplication primarily for **Linear Transformation** (which is the building block of Machine Learning Models), which we will explore in later posts. Though it can be a bit non-intuitive, the way matrix multiplication is defined works greatly in ordering things neatly!
