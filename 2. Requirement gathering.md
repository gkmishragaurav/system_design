#### Purpose:
The purpose of requirement gathering is to test your ability to clarify an open-ended and ambiguous problem statement. Sometimes the problem statement could be as vague as Design a ridesharing service. The interviewers want to see if you can organize your thoughts and focus on a set of requirements. Then you should finalize the system’s assumptions with the interviewers, so you can focus on them for the rest of the session.
- Functional Requirements:
- Gathering Features:
  - During this section, act as a product manager and develop user stories to solve the users’ problems. Even though we’re software engineers, interviewers do look for solid product sense and strong user empathy. When given a question, think about:
	  - Who is it for, and why do we need to build it?
	  - What are the features we need to solve the users’ problem?
- For more infrastructure and backend problems, still take a moment to think about the end-users’ experience. For example, if you’re designing a web crawler, you want to ask how important the freshness is to the user. If the crawler is supposed to support a breaking news website, the freshness needs to be a lot more urgent.
- After you’ve come up with a couple of features, narrow them down to just 1 or 2 and get the interviewers’ buy-in. In real life, each feature could take months, if not years, to build. If you focus on too many features, the session will just be breadth focused. You should ask which features the interviewer is interested in. Typically, the interviewer will narrow down to a selected few. 

#### ================== Example ================
- Q. Please design a file storage system?
  - Don't do this:
    - Candidate:
      - Can I assume the user can save the file into a cloud storage and they should also be able to view the files in a dashboard?
    - Interviewer:
      - Yeah sure, and the users would like to view their files in a file-system-like dashboard.
    - Candidate:
      - Ok, we will need to create folders and each folder should have files and folders
  - Do This:
    - Candidate:
      - Why are we building file storage? What is the customer problem we’re trying to solve?
    - Interviewer:
      - The users would like to organize their local files into the cloud with the same folder-like structure. They want to ensure they don’t lose the photos and would like to occasionally browse their files.
    - Candidate:
      - Ok, to solve that customer pain point, we can have a feature where the user can click and drop a folder and we will recursively upload the folders and files within it. And here’s a wireframe of what I think the end-user should see. We will ensure the system has strong durability
  - Analysis:
    - Even though both approaches lead to similar APIs that create and view files, the latter approach demonstrates much stronger user empathy. You’re suggesting features to solve customer problems rather than just coming up with random features that seem related. Because you understand the product, you can leverage it by claiming the importance of the durability of your system since users won’t like to lose their life memories.
  - Do This:
	  - Here are the features I think we can go with to solve the customers’ problem:
		  - Users can request a ride and we will match them with a nearby driver.
		  - Users can view all the nearby drivers.
		  - Users can receive estimated payments.
		  - Users can pool with other riders.
	- For now, I will focus on feature #1 and expand further if needed, are you ok with that?

#### ========================================================

- Non-Functional Requirements:
	- After you agree on the features, identify areas that make your design unique and challenging. You should ask questions to build preliminary tuition on what could break your system and, when it does, some areas that can be compromised to scale for those bottleneck challenges. Also, asking good questions gives interviewers good data points about how you think about the design by focusing on what matters.
	- Scale:
		- How Many Active Users Are There in the System?
			- The goal of this question is to figure out the scale of the system. Sometimes you might need to adjust the question to fit the context of the interview design question. For example, if the interviewer asks you to design a web crawler, you might want to ask how many URLs and pages you have to crawl. You can use this number to build the intuition on the scale and calculate the math.
		- How Are the Users Distributed Across the World?
			- Globally, different users access applications as the world becomes closer together through the internet. Unfortunately, the latency for cross-globe communication may significantly impact the user experience. Therefore, it’s crucial to figure out the distribution to discuss geo locality design in the deep dive section.
		- What Are Some Scenarios That Could Lead to High QPS(Queries-per-second)?
			- The goal here is to demonstrate your ability to think of scenarios that can break your system. One example is bursty situations that cause a thundering herd problem. Just as in real life, when there’s a design proposal, you look for real-life scenarios that may cause headaches for your system. Not only do you demonstrate experience by considering the worst case, but it also brings up deeper design considerations with interesting trade-offs that will leave the interviewers with stronger impressions. A design without bottlenecks isn’t challenging and interesting. You should be the candidate who proactively comes up with difficult cases instead of waiting for the interviewer to provide them.

#### ================== Example QPS Bottleneck ================
- Q. Design a Ridesharing Service
	- Should I consider cases where users get out of a concert event and a significant number of people are trying to book for rides?
- Q. Design Facebook Live Streaming:
	- Should I worry about events like royal wedding where there could be tens of millions of people trying to enter the stream at the same time?
- Q. Slack:
	- Should I worry about supporting a company level chat room that has tens of thousands of employees where there may be a lot of chats?
- Q. Design E-Commerce:
	- Should I worry about the situation where many buyers try to buy an item at the same time leading to inventory problems?
#### ========================================================
- What Are Some Scenarios That Could Lead to High Storage and Bandwidth?
	- The goal here is to figure out what kind of pattern could cause the system to have high storage and bandwidth such that you need to scale the storage system. One factor is the amount of memory passed through a request and how frequently the servers handle the requests.
#### ================== Example of Storage Bottleneck ================
- Q. Design a Photo Storage
	- Are there super users who upload more photos than an average user?
- Q. Design a Cloud File Storage System
	- Are there users who upload large files in the magnitude of GB?
- Q. Design Slack with Image and Video Sharing
	- Since slack is used during work hours, can I assume that there will be a lot more images and videos sent during those hours and scale for that?
- Q. Design Netflix
	- Can I assume users like to watch movies at night and anticipate bigger traffic during those hours? Can I assume there is only a small subset of popular movies most people like to watch?

#### ========================================================

- Performance Constraints:
	- Remember, if the world ran on supercomputers with no network latency, computers would never go down, and with unlimited storage, we would not have to worry about distributed systems. However, things do break, and networks do get congested. To achieve the scale that we need, we may have to make sacrifices to our system. You should discuss and agree with the interviewer on the constraints before proceeding further. Here are some high-level idea aspects to consider:
- What is the Availability and Consistency Requirement?
	- The goal here is to discuss whether the system can tune the user product experience’s consistency to meet the availability demand better. A common mistake candidates make is to be too solution-focused, where candidates begin talking about choosing an AP system (CAP Theorem) over the CP system. Focus on the user experience instead.

#### ========================= Example ======================
- Interviewer:
  - Q. Please design Facebook Newsfeed
  - Don’t Do This
	  - I will choose AP system over CP system because we need the newsfeed product to be highly available and it is ok to be inconsistent.
  - Do This
	  - When a user posts a feedback, can I assume that it is ok to have some delay before the user’s post shows up in other users’ feed in case I need to optimize for availability?
  - Analysis:
	  - In the Don’t example, it’s unclear which part of the system should favor availability over consistency. In a system, there could be components that are CP and other components that are AP. You need to be clear on the use cases. Even if every feature within it should be AP, there is much more clarity if you describe the user experience.
#### ========================================================

- Q. What Is the Accuracy Requirement?
	- Similar to consistency, the goal here is to discuss whether the system can sacrifice accuracy to meet the design constraint better. Accuracy is different from consistency. For example, eventual consistency is eventually accurate where inaccuracy implies the processed data doesn't have to be the same as what the users provided. Yet, the design still offers a good user experience.
	- For example, you should ask whether or not it is ok for a notification service to drop some messages. Is it ok for rate limiters to be approximately correct? Is it ok for stream processing to consider most of the events but drop the late events? There can be room for creativity here, and coming up with a clever idea will give you bonus points.

- Q. What Is the Response Time and Latency Constraint?
	- The goal here is to figure out how long the users have to wait before receiving the expected data and still deliver a good user experience. Different applications have different response time requirements.
	- For example, it might be acceptable for an airline booking system to take more than 5–10 seconds, but it is not acceptable to render the Facebook News Feed to take more than 500 ms in p99 of the use cases.

- Q. Latency and responce time
	- People often confuse latency with response time. However, from the end-users’ experience, we want the response time, not latency, because that’s how long the users have to wait before they get a response.
	- Response Time = Latency + Processing Time
	- Response Time: The time difference between the client sending the request and receiving the response.
	- Latency: The time the request has to wait before it is processed.
	- Processing Time: The time it takes to process the request.
	- Response Time is always more than Latency. However, most APIs are just simple pass-throughs to fetch for something light with little processing time and thus Response Time ~= Latency.

- Q. What Is the Freshness Requirement?
	- The goal here is to figure out how data staleness will impact the user experience. Data freshness categories are real-time, near-real-time, and batch processing. Of course, there isn’t an exact definition of each category, and the point is to articulate how each impacts the system you’re designing.

#### ========================= Example ======================
- Real-Time:
	- A stock trader sitting at home needs the data to be real-time because a delay in the price feed may cause the trader to make the wrong trading decision.

- Near Real-Time:
	- When a celebrity is streaming their experience at a baseball game on Facebook Live, the stream itself should be near real-time, but a couple of seconds delay is acceptable. The users won’t feel a difference with a couple of seconds delay, but if the stream is delayed by a couple of hours, some users will likely find out because the game is already over.

- Batch Process:
	- Because real-time and near real-time systems are challenging and expensive to build, some applications can still have a good user experience even if it takes a couple of hours or days to run. For example, a static website’s web crawler for search does not need to be updated often.

#### ========================================================

- Q. What Is the Durability Requirement?
	- Here the goal is to figure out how data durability will impact the user experience. In the event of a data loss, how will the user feel? Service level agreement measures durability in 9s. For example, nine 9s will mean 99.999999999%, which means in a year, the storage will lose 0.000000001% of the data. Don’t worry too much about the exact number of 9s in the interview, you can just stress the importance of data loss with respect to the end-user.
	- High Durability:
		- When you’re storing users’ life photos, it is extremely important to be highly durable. Losing a photo would mean never being able to see that moment of their life again. So, in the interview, you should emphasize the importance of durability design to prevent correlated failures.
	- Medium Durability
		- For casual chats that happened years ago, you might argue that the users will rarely look at the ancient chat history again. While the chat history is still important to be durable, losing a message that happened years ago wouldn’t get a user super angry
	- Low Durability
		- For a rich sharing service to capture drivers’ location, it is acceptable if we lose a driver’s location for a moment in time because we will get their location for their next update in the next few seconds. So losing location data wouldn’t result in many impacts on the underlying system.

