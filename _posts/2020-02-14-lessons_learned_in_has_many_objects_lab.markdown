---
layout: post
title:      "Lessons Learned in Has Many Objects Lab"
date:       2020-02-14 15:41:39 -0500
permalink:  lessons_learned_in_has_many_objects_lab
---


The Has Many Objects Lab gave me a better perspective of how objects in different classes can relate. It forces one to pay more attention to detail on how to write the lines of code that can support this interdependency. Without the code linking related classes, one can write perfect lines of code for one class. However, upon running tests you will get a lot of errors if the lines which were supposed to link the classes are incorrect or have not been linked by respective code in the related class.
When dealing with object relationships it is easy to get confused figuring out what object(s) belongs to what class, so I decided right at the beginning to use learn –f-f (learn fail fast) method to run the tests. The learn –f-f method stops running the tests once the first failed test is encountered. The advantage of doing this was that the lab would not be so intimidating or overwhelming as I was dealing with it one step or test at a time. However, this called for patience to navigate back and forth between the four different classes and their respective specs. This back and forth scenario can be seen in the examples below.
When I wrote the code for the Artist class’s #songs instance method, I got an error. (See both below).

```
def songs
    Song.all.select {|song| song.artist == self}
 end

```

```
Failure/Error: Song.all.select {|song| song.artist == self}
 NameError:
       uninitialized constant Artist::Song
     # ./lib/artist.rb:7:in `songs'

```

This signaled that I needed to switch to the Song class where I did set up the attribute accessors, #initialize instance method, and .all class method (which is self.all) to resolve the above error.
In defining the #song_count instance method I had the presence of mind to tie the code to the Song class:

```
def self.song_count
    Song.all.count
  end

```
At this point, the Artist class is done and it is time to move to the Author class!!
The code for the #posts instance method in Author class did not pass the test until I had to fully define ‘author=’ methods in the Post class. Another switch to a different class to create the relationships between objects: posts and author. After initializing and adding author to Post class attribute accessors, the #posts instance method in Author class passed the test.
Finally, I should point out that I had some difficulty writing the code for the #author_name instance method in the Post class. The spec requirements for #author_name was: 
(1). belongs to an author, and 
(2). knows the name of its author. 
My initial wrong code:

```
def author_name
      self.author.name
  end

```

This code returned an error that it did not return nil if the post does not have an author. The eventual correct code was:
```
def author_name
    if self.author
      self.author.name
    else
      nil
    end
  end

```

This is the lab where I also learned how to comment out multiple lines of code or comments by highlighting the lines then hitting "Ctrl"+"/". In the end, all the 28 tests turned green! Such a great feeling for the successful journey that began with a single step using learn –f-f test method.

