---
layout: essay
type: essay
title: "AI's Role in Software Engineering Education"
# All dates must be YYYY-MM-DD format!
date: 2024-04-28
published: true
labels:
  - AI
  - Programming
  - Software Engineering
  - Learning
  - interests
  - skills
---
<img width="300px" class="rounded float-start pe-4" src="../img/smart-questions/ AI.png">

Artificial Intelligence (AI) is revolutionizing software engineering education, making it more efficient and interactive. AI-powered tools like ChatGPT and GitHub Copilot are equipping students with a competitive edge, providing a glimpse into the future of technology. By integrating AI into software engineering education, we are nurturing a new generation of engineers who are confident in their ability to tackle the tech challenges of tomorrow.
Here are my experiences with AI in different aspects of software engineering education:

1.	Experience WODs (E.g., E18): I did not use AI for the Experience WODs, as they come with comprehensive explanations and follow-up steps, making additional AI assistance unnecessary. 
2.	In-class Practice WODs: I used AI to speed up the process of writing code, since these exercises have time constraints and speed is crucial.
3.	In-class WODs: Similar to practice WODs, I relied on AI to write code more quickly to cope with the time limitations during these sessions.
4.	Essays: I utilized AI to summarize articles, which made it easier for me to extract relevant information and incorporate it into my essays effectively.
5.	Final Project: I employed AI to detect errors in my code, which proved to be immensely helpful, enhancing both efficiency and accuracy in debugging.
6.	Learning a Concept / Tutorial: I attempted to use AI to learn new concepts and follow tutorials, but it was not as effective as I expected. Consequently, I turned to other platforms for better explanations.
7.	Grammar Review: I consistently use a grammar AI tool to check and refine my grammar before responding to questions on Discord, ensuring clarity and correctness in my communications.
8.	Asking or Answering a Smart Question: I tried using AI to ask or answer complex questions but found the responses inadequate. This led me to seek clarification directly from my instructor.
9.	Coding Example (E.g., using Underscore .pluck):
    
Coding Example: Error Detection and Solution in React

Background: While working on a React project, I encountered a bug related to state management that caused the UI to not update correctly after state changes. This problem appeared under complex scenarios such as conditional rendering or during asynchronous operations.

Problem Code:
```jsx

import React, { useState } from 'react'; function Counter() { const [count, setCount] = useState(0); const increment = () => { setCount(count + 1); }; return ( <div> <p>{count}</p> <button onClick={increment}>Increment</button> </div> ); }

```

Issue Description: I was struggling to understand why the counter wasn't updating under certain conditions, which complicated debugging efforts.
AI-Assisted Solution: I discussed the issue with AI (specifically, ChatGPT), providing details about when the problem occurred and the symptoms. The AI suggested several 

### troubleshooting steps:
- Functional Update: It recommended using a functional update form for setCount to ensure the count updates correctly based on the previous state, which is crucial in complex scenarios:

```
const increment = () => { setCount(prevCount => prevCount + 1); };
```

- Dependency Check: The AI advised checking all dependencies in any useEffect hooks to ensure they are correctly listed, addressing potential issues related to effect misfires.

### Outcome: 
This guidance helped me think through the problem systematically, providing both specific coding solutions and general best practices. It significantly enhanced my understanding and efficiency in debugging, showcasing the practical benefits of AI in software development.

11.	Explaining Code: I regularly use AI to help document and explain my code. Its ability to clarify complex logic in simple terms makes my code more understandable to others.
12.	Writing Code: AI has been used to assist in writing my code, whether through suggesting snippets or completing lines of code.
13.	Documenting Code: I use AI to enhance my code documentation. It helps in explaining what specific functions or blocks of code do, which is beneficial for both my understanding and that of future readers.
14.	Quality Assurance (E.g., identifying issues or fixing ESLint errors): AI has been applied to identify errors or quality issues in my code, such as linting problems or logical errors.
    
AI tools have been instrumental in enhancing my understanding of complex software engineering concepts. Specifically, while building websites using React, ChatGPT's assistance in debugging and understanding nuanced aspects of React state management and component lifecycle has significantly accelerated my learning curve. I am now able to grasp intricate details that would have otherwise required more time and effort to understand.

In addition to error detection, GitHub Copilot's real-time suggestions of code snippets and best practices have helped me in quickly learning syntax and libraries. Adopting industry-standard coding patterns has improved my coding skills and adaptability, making me a more efficient and effective software developer.

Although I have not yet had the opportunity to apply AI tools in real-world software engineering projects outside of my ICS 314 class, my experiences within the course have clearly demonstrated the potential benefits of AI integration. These classroom encounters have equipped me with a foundational understanding of how AI can enhance software development processes, including debugging, code optimization, and automated testing. I am confident that AI-powered tools will continue to play an increasingly important role in software development, and I look forward to exploring their full potential in the future.

### Future Plans and Anticipated Benefits: 
Looking forward, I am eager to incorporate AI tools like GitHub Copilot and AI-powered testing frameworks in my future projects, internships, or hackathons like the Hawaii Annual Code Challenge (HACC). I anticipate that the use of these tools will allow for:
•	Increased Efficiency: By automating routine coding tasks, I can focus more on creative aspects of software development and problem-solving.
•	Enhanced Code Quality: AI's ability to detect bugs and suggest optimal coding practices could help in maintaining a high standard of code quality.
•	Innovative Problem Solving: With AI’s assistance in handling complex algorithms or data analysis, I can engage more deeply with innovative solutions to challenging problems.

•	Challenges: The reliance on AI for problem-solving could inhibit critical thinking and skill development in students. Additionally, AI tools might not always provide accurate or complete information, which could lead to misconceptions.

### Opportunities:
•	Interactive Learning: AI can create personalized and interactive experiences, like real-time feedback on coding projects.
•	Automated Testing: AI can improve automated testing systems, helping students write more robust code.
•	Collaborative Projects: AI can enhance collaboration on group projects by efficiently managing and merging contributions.

### Traditional vs. AI-Enhanced Teaching Methods:
•	Engagement: AI-enhanced methods, such as interactive coding sessions, offer more hands-on experiences, increasing student engagement compared to traditional lectures.
•	Knowledge Retention: AI tools can adapt to individual learning paces and styles, improving knowledge retention.
•	Skill Development: AI methods provide practical applications and real-world problem-solving, enhancing skill development beyond traditional teaching.

### The future of AI in software engineering education involves:
•	Ethical Considerations: Educating students on the ethical use of AI, including privacy and bias concerns.
•	Balance Between AI Assistance and Foundational Skills: Ensuring AI aids without replacing the development of essential skills.
•	Continual Updating of AI Tools: Keeping AI tools up-to-date with industry changes to maintain relevance.

The role of AI in education is expanding and offering promising benefits for interactive and effective learning. The integration of AI into software engineering education has been found to be profoundly beneficial, making learning more efficient and engaging while preparing students for the complexities of tomorrow's technological challenges. As AI continues to permeate various facets of education and industry, we must explore its potential responsibly while ensuring that it complements fundamental engineering skills and enhances overall human capability. It is crucial to balance the use of AI in education to ensure that students continue to develop fundamental skills and ethical understanding. With proper implementation, AI will revolutionize the education sector, offering new and exciting opportunities for students to learn and grow.
