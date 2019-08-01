---
layout: post
categories: [Java, C++]

I need to learn C++ in college course. I tried to avoid C++ because I did not like “cout << variables;” and I somehow did not need it because I knew C (basic expressions and pointer, structure, etc..) a little bit. I am actually having fun to learn C++.

# In Java

Learning new things brings a lot of questions, which is good. Now I have a question among vector, array, and list in C++. My understanding in Java is that List is an interface, ArrayList is a class that implements List interface, and Vector class is also a class that implements List interface. The difference between ArrayList and Vector classes is **ArrayList is not synchronized** but Vetctor is.

# In C++

According to A tour of C++ (Bjarne Stroustrup, 2018), vector’s “elements are stored contiguously in memory” while list is “**a doubly-linked list**” that its element has pointers to predecessor and successor. So **vector performs better than list for traversal, sorting and searching**. The book said that “Unless you have a reason not to, **use a vector**“. It seems that C++ standard library offers singly-linked list called forward_list as well.

Categories: Java, C++