---
layout: post
title: Usefulness of constexpr in C++14
description: With the advent of C++14, can users of established languages like C++ enjoy CTFE of D programming language?
thumbnail: /media/images/usefulness-of-constexpr.jpg
---
![Usefulness of constexpr in C++14]({{baseurl}}/media/images/usefulness-of-constexpr.jpg)
**With the advent of C++14, can users of established languages like C++ enjoy CTFE of D programming language?**

The new standard of C++, that was formally called C++1y has been released for preview in the [mid-August](http://isocpp.org/blog/2014/08/we-have-cpp14) of 2014. It took some time for the standardization. [Clang](http://clang.llvm.org/cxx_status.html) and [g++](https://gcc.gnu.org/projects/cxx1y.html) already implemented most of its features at the time with Clang claiming to be 100% feature-complete. For the new users of C++11, it merely enhances some aspects that were either oversight or voluntary left out for the future revisions.

One of many things that C++11 introduced is the inclusion of [compile-time function evaluation (CTFE)](http://en.wikipedia.org/wiki/Compile_time_function_execution) in the core language through the use of `constexpr` keyword. It is noted that we have already seen CTFE in [D programming language](http://dlang.org/
) — a language that is highly influenced by C++, through which with small intuition, we can evaluate lots of things at compile-time. While `constexpr` in C++ is arguably far less powerful than CTFE features found in D, it still provides some ways to evaluate various things at compile-time.

In C++11, not more than simple arithmetic with numbers or finding min/max values of `int` could be done with `constexpr`. C++14 improves upon it; it relaxes a lot of its restrictions, namely some iterations can now be done within a function without resorting to doing recursion for looping. We will see what can be done easily with C++14 that were previously cumbersome to be done with C++03/C++11. Although, I have mentioned about CTFE of Dlang, I won't write about it in this post.

## Variable initialization

In C++11, we couldn't initialize variables in a `constexpr` function, which greatly limited its usefulness. With C++14, we can simply initialize how many variables we need, though we can’t use **static**, **thread_local** and **global** variables.

{% highlight C++ %}
constexpr auto add(int a, int b) {
	int c = a;
	int d = b;
    return c + d;
}

int main() {
    int a = add(20, 20);
}
{% endhighlight %}

## Conditional branch

We can now use **If** and **else** in `constexpr` functions, if they don’t have any extra return statement. Previously we had to use the short form of if/else to achieve the same effect.

{% highlight C++ %}
constexpr auto min(int a, int b) {
    if (a < b) {
        return a;
    }
    else {
        return b;
    }
}

int main() {
    constexpr int array[2] = {4,5};
    auto n = min(array[0], array[1]);
}
{% endhighlight %}

## Loops / Iterations

With C++14, we can write loop statements for iterations. This also includes **range-based for loops**. Previously, we had to use recursion to achieve the same effect.
{% highlight C++ %}
constexpr auto add_into(int a, int b) {
	for (int i = 0; i < 10; i++) {
		a += b;
	}

	return a;
}

int main() {
    int a = add_into(20, 20);
}
{% endhighlight %}

## Conclusion

C++’s compile-time evaluation features have a long way to come near Dlang's CTFE, but they are arguably in the right direction. I have already seen its uses in new libraries. If you are using new `constexpr` features in your C++ library, then please tell me in the comments section!
