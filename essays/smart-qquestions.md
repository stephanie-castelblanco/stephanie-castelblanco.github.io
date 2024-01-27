---
layout: essay
type: essay
title: "Mastering Smart Questions: A Guide for Effective Technical Support"
# All dates must be YYYY-MM-DD format!
date: 2024-01-25
published: true
labels:
  - Questions
  - Answers
  - StackOverflow
---

<img width="350px" class="rounded float-start pe-4" src="../img/dumbcartoon.png">


## What’s a smart question?
Asking a smart question involves taking the time to think through the problem at hand and understanding what information is necessary to solve it. It's more than just collecting data, but also requires a thoughtful and strategic approach to problem-solving, promoting trust and cooperation among everyone involved, and contributing to a constructive and successful resolution process.

###  Prioritizing Research: A Critical Step Before Seeking Assistance
As a software developer, we might encounter difficulties while navigating the complex software development landscape. Seeking technical assistance is an essential part of our journey, and we can make the process more effective by following specific guidelines outlined in "How to Ask Questions the Smart Way" by Eric Raymond. This essay will explore the importance of asking smart questions, evaluate the chosen questions against established precepts, analyze the responses in terms of smartness, and share insights gained from this experience.

Raymond's first guide is to exhaust all available resources for self-discovery before reaching out for assistance. This involves using search engines like Google, specialized platforms such as forums, and manual users and checking Stack Overflow for similar questions that have already been answered. As a last resort, one can ask in Stack Exchange. Stack Overflow is an excellent resource for programming-related queries, while Super User caters to general-purpose computing questions. This initial step ensures that the questioner has made a genuine effort to understand and resolve the issue independently.

The foundation of effective collaboration lies in respecting the time and expertise of those who might provide assistance. Engaging in hands-on learning and exhaustive research before seeking help reflects a proactive approach and creates a positive learning environment. This respect for the efforts of others fosters a culture of mutual respect, which is essential in the collaborative world of software engineering.

## Let's examine two scenarios, one where the question aligns with smart questioning practices and another where it does not:


### * Smart Question: 
* In the following example, we examine the components of a decent question. In this case, the asker is trying to figure out why processing a sorted array is faster than processing an unsorted array.

"Why is processing a sorted array faster than processing an unsorted array?” The questioner has provided the code they have tried, their research and their question. This question follows the principles of smart questioning, as it is specific, includes relevant details, and demonstrates the questioner's troubleshooting efforts. It is expected to receive thoughtful and targeted responses.

Code provided with the question:

```
In this C++ code, sorting the data (before the timed region) makes the primary loop ~6x faster:

#include <algorithm>
#include <ctime>
#include <iostream>

int main()
{
    // Generate data
    const unsigned arraySize = 32768;
    int data[arraySize];

    for (unsigned c = 0; c < arraySize; ++c)
        data[c] = std::rand() % 256;

    // !!! With this, the next loop runs faster.
    std::sort(data, data + arraySize);

    // Test
    clock_t start = clock();
    long long sum = 0;
    for (unsigned i = 0; i < 100000; ++i)
    {
        for (unsigned c = 0; c < arraySize; ++c)
        {   // Primary loop.
            if (data[c] >= 128)
                sum += data[c];
        }
    }

    double elapsedTime = static_cast<double>(clock()-start) / CLOCKS_PER_SEC;

    std::cout << elapsedTime << '\n';
    std::cout << "sum = " << sum << '\n';
}
Without std::sort(data, data + arraySize);, the code runs in 11.54 seconds.
With the sorted data, the code runs in 1.93 seconds.
(Sorting itself takes more time than this one pass over the array, so it's not actually worth doing if we needed to calculate this for an unknown array.)

Initially, I thought this might be just a language or compiler anomaly, so I tried Java:

import java.util.Arrays;
import java.util.Random;

public class Main
{
    public static void main(String[] args)
    {
        // Generate data
        int arraySize = 32768;
        int data[] = new int[arraySize];

        Random rnd = new Random(0);
        for (int c = 0; c < arraySize; ++c)
            data[c] = rnd.nextInt() % 256;

        // !!! With this, the next loop runs faster
        Arrays.sort(data);

        // Test
        long start = System.nanoTime();
        long sum = 0;
        for (int i = 0; i < 100000; ++i)
        {
            for (int c = 0; c < arraySize; ++c)
            {   // Primary loop.
                if (data[c] >= 128)
                    sum += data[c];
            }
        }

        System.out.println((System.nanoTime() - start) / 1000000000.0);
        System.out.println("sum = " + sum);
    }
}
With a similar but less extreme result.

My first thought was that sorting brings the data into the cache, but that's silly because the array was just generated.

What is going on?
Why is processing a sorted array faster than processing an unsorted array?
The code is summing up some independent terms, so the order should not matter.

```

The asker received twenty-five possible answers, responders were more likely to engage with the question due to its clarity and the evidence of the questioner's research efforts. As a result, the ensuing discussion is anticipated to be productive and conducive to problem-solving. Link to the question: https://stackoverflow.com/questions/11227809/why-is-processing-a-sorted-array-faster-than-processing-an-unsorted-array/11227902#11227902


### Non-Smart Question:

The way to get ignored is by asking non smart questions. In contrast, the non-smart question states, "The image upload code is not working." They are missing a crucial detail: the error message they received. This shows that the person did not put in any effort to understand or solve the issue by themselves.

Code provided with the question:

```
image upload code is not working

public function store()
    {
        $rules=array(
              'gallery_name'=>'required',
              'image_title'=>'required',
              'image'=>'required'
        );
        $file = Input::file('image');
        $destinationPath = 'uploads/';
        // If the uploads fail due to file system, you can try doing public_path().'/uploads' 
        $filename = str_random(32) . '.' . $file->getClientOriginalExtension();
        //$filename = $file->getClientOriginalName();
        //$extension =$file->getClientOriginalExtension(); 
        //get all book information
        $galleryInfo = Input::all();
        //validate book information with the rules
          $validation=Validator::make($galleryInfo,$rules);
          $upload_success = Input::file('image')->move($destinationPath, $filename);
          if($validation->passes())
          {
          //save new book information in the database 
          //and redirect to index page
              if ($upload_success) {
                    //save in the Band table database
                    Gallery::create($galleryInfo);
                            return Redirect::route('galleries.index')
                             ->withInput()
                             ->withErrors($validation)
                             ->with('message', 'Successfully created Gallery.');
                    }   
                     else {
                           return Redirect::route('galleries.create')
                           ->withInput()
                           ->withErrors($validation)
                           ->with('message', 'Image fields are incomplete.');
                    }
          }
          //show error message
          return Redirect::route('galleries.create')
               ->withInput()
               ->withErrors($validation)
               ->with('message', 'Some fields are incomplete.');
     } 

```

The asker only recieved one response asking for more details. Answering this type of question can be challenging for responders since they don't have sufficient information to provide helpful assistance. They might ask for more details, which can cause delays and discourage the person from seeking help. Overall, due to the vagueness of the question, the chances of a positive outcome are low. Link to the question: https://stackoverflow.com/questions/28462190/image-upload-code-is-not-working


### Insights Gained: When evaluating smart and non-smart questions, I have learned several valuable insights:

* Effort Precedes Assistance: 
Questions that demonstrate the questioner's effort and understanding receive more constructive and helpful responses. It is important to put in the work before seeking help.

* Choose the Right Forum: 
To optimize efficiency and effectiveness, it is important to choose the right forum for technical help online. Follow up on solutions provided and contribute to the forum's collective knowledge. 

* Effective Communication is Crucial: Clear, courteous, well-formulated questions increase the chances of receiving valuable assistance and foster a positive learning environment.

* Community Participation is Reciprocal: Active participation in forums and communities contributes to a collaborative atmosphere, creating a network of support for software engineers.

## Conclusion
Eric Raymond's article "How to Ask Questions the Smart Way" has been an excellent guide for me, a newcomer in software engineering, to avoid misunderstandings with advanced hackers on the web. In the field of software engineering, asking intelligent questions is not just a skill but a guiding principle that shapes collaborative learning and problem-solving. By adopting smart questioning practices, software engineers can effectively seek technical assistance while contributing to a positive and supportive community. The insights I gained from this experience emphasize the reciprocal nature of collaboration and the importance of proactive, respectful engagement in the dynamic world of software development.

<img width="400px" class="rounded float-start pe-4" src="../img/dumb.png">
