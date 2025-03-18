# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```



Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.

 #### I've deduced that $T(n) \in O(n^{5})$ by this reasoning:

##### The steps of this algorithm are:
1. If the array has 0 or 1 elements, stop (base case). This step has a time complexity of $T(1)=1$
2. Recursively divide the array by 3, initialize the count, then recursively divide the array by 3 again. This step has a time complexity of $T(n) = 2T(n/3)$
3. For loop on $n^{2}$. $T(n) = n^{2}$
	* For loop on $n$. $T(n) = n$
		* For loop on $n^{2}$. $T(n) = n^{2}$
4. Recursively divide the array by 3 again. This step has a time complexity of $T(n) = T(n/3)$

###### RECURRENCE RELATION:
$T(n)=1$ if $n \le 1$
$T(n) = 3T(\frac{n}{3})+n^{5}$ if $n>1$

To find big-O of $T(n)$, we must repeatedly substitute $T(n)$ into itself, find how $T(n)$ changes with each substitution, and simplify $T(n)$ so that it does not depend on itself.

$T(n)$ changes with each substitution by $3^iT(\frac{n}{3^i})+\sum_{k=0}^{i} 3^{k}\cdot (\frac{n}{3^{k}})^5$ which is equivalent to $3^iT(\frac{n}{3^i})+n^{5}\sum_{k=0}^{i} \cdot \frac{1}{3^{4k}}$, where $i$ is the number of iterations before reaching the base case. Because we are dividing the input size by 3 with each iteration, there should be $log_{3}n$ iterations before reaching the base case. Substituting $log_{3}n$ for $i$, we can simplify $3^{log_{3}n}T(\frac{n}{3^{log_{3}n}})$ to $n$ since $3^{log_{3}n}=n$ and $T(\frac{n}{3^{log_{3}n}})$ = 1.  That leaves us with $n+n^{5}\sum_{k=0}^{i} \cdot \frac{1}{3^{4k}}$, who's big-O complexity is just $n^{5}$ since $n^5$ dominates the constant factor that the summation converges to and the linear factor $n$.

Therefore, $T(n) \in O(n^{5})$

"I certify that I have listed all sources used to complete this exercise,
including the use of any Large Language Models. All of the work is my own, except
where stated otherwise. I am aware that plagiarism carries severe penalties and
that if plagiarism is suspected, charges may be filed against me without prior
notice."