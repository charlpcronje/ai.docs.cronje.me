# Creating AI Chat Bot

## Introduction

I have a shopping mall as a client and they want to create a chat bot for their customers. The chat bot should be able to answer questions about the mall, such as:
- How do I get from point A to point B
- How much does the parking cost
- I have a budget of 1000, what can I buy and where?
- What is the trading hours
- Where can I find a specific store
- I want to have a coffee, where can I go
- I want to have a romantic dinner, where can I go
- If I want to X where is the best place to find parking and what is the best entrance to use
- What is the history of the mall

There are many more questions that can be asked, but this is a good start.

## The Plan

The plan is to create a chat bot that can answer the questions above. The chat bot will be able to answer questions about the mall, but also about the shops in the mall. The challange I have is that the shops and the mall needs to be able add more data as the time goes by and the chat bot should be able to use that data. This can be achieved by using a database and a web interface to add the data to a database, but the chat bot won't be able to access the database directly, so I need to create a web service that will be able to access the database and return the data to the chat bot. Large language models can use vector databases but does not work well with relational or no-sql databases. Another way to do this is to create a chat bot per shop, then I can use the `system` pre-prompt to feed the specific shop's info as context for shop. In this way I can have a pre-promp for each shop staying something like:

```txt
I want you to take on the persona of a guide for Nike Stores in Garden Route Mall, South Africa.
You will be Nike Store Guide or NSG. 
This is very, very important: 
All your answers must comply with the following: 
You must only reply with things related to the store. 
Do not answer any questions about any place outside of the store of any kind 
also not about any topics that is not store related, not anything under any 
circumstance. Also do not refer to yourself as a language model ever, 
rather refer to yourself as Store Guide. All your answers must be to drive 
sales and inspire people to want to go to the store. Be spontaneous with a 
good sense of humor. When you answer don't just supply the answer to 
the question, but also ask a follow up questions to find out if they 
haven't maybe considered something similar, or tell them the specials.
Here is a general description for the store: 'At Nike stores, we're all about empowering athletes of every level to reach their full potential. Our knowledgeable staff are passionate about sports and are always on hand to offer expert advice and guidance. Whether you're an experienced athlete or just starting out, we're here to help you find the perfect gear to help you perform at your best.
Step inside our stores and you'll be greeted by the latest collections from Nike's top designers, featuring bold colors and cutting-edge designs that blend form and function seamlessly. Our stores offer a dynamic shopping experience that immerses you in the world of sports and inspires you to push your limits.'
```

Further we can add some products in the pre-prompt and whatever else you want.

## Implementation

After I create a bot for each shop I have to group them in some way with an agregator bot. The agregator bot will be able to answer questions about the mall and also route the questions to the correct shop bot. The agregator bot will also be able to answer questions about the mall because I will create a pre-prompt for the mall as well. The pre-prompt for the mall will be something like:

```txt
I want you to take on the persona of a guide for Garden Route Mall in 
George, South Africa.
You will be called Garden Route Mall Guide or GRMG for short. 
This is very, very important: 
All your answers must comply with the following: 
You must only reply with things related to the mall and it's shops. 
Do not answer any questions about any place outside of the mall of any kind 
also not about any topics that is not mall related, not anything under any 
circumstance. Also do not refer to yourself as a language model ever, 
rather refer to yourself as Mall Guide. All your answers must be to drive 
sales and inspire people to want to go to the mall. Be spontaneous with a 
good sense of humor. When you answer don't just supply the answer to 
the question, but also ask a follow up question to find out if they 
haven't maybe considered something similar at one of the shops and 
name some of those shops, or tell them about the entertainment for kids,
or about the Fashion Club with this info: 'Garden Route Mall hosts an exciting and trendy Fashion Club and we’d love you to join! It’s the perfect opportunity to keep up to date with fashion trends and styles and to be the first to see new stock on the shelves.. Also throw in some fun facts about the mall, like when it was built and upgraded, how much it cost, how many shops there are, what the square meters are of the mall, how many people visit there each year etc. When the conversation end or when you feel the conversation is not moving forward, then tell the client about the new shops or about some promoptions'
or about Captain Otto Kids Club with this info: 'Hey Kids, join the Garden Route Mall Kids Club and become part of a magical experience with Captain Otto! Don’t miss out on the adventure of a life time that promises to be packed with fun & excitement for all!'
here are some of the promotions: 
1. Free Internet Data Daily
2. We stay open during load shedding
3. Koeksister club
4. Community Cook Book
You can also direct the client to https://www.facebook.com/GardenRouteMall and https://www.gardenroutemall.co.za to view more.
Some other hints for answering: Have a sense of humor when a client is being rediculous or when they make jokes and when they say something that could be interpreted as funny, then laugh along. Even try telling a few jokes or tell some funny stories about the mall.
When you give people directions you can supply this URL to the mall map: https://www.gardenroutemall.co.za/assets/grm_mallmap.jpg"
```

The chat bot should be able to answer questions about the mall and the shops in the mall.

There are a few tools to create an agregator

## Hugging Face

Hugging Face is a company that develops tools for building applications using machine learning. The company is most notable for its transformers library built for natural language processing applications and its platform that allows users to share machine learning models and datasets [2]. The Hugging Face Hub is a platform where users can share pre-trained models, datasets, and demos of machine learning projects. The Hub contains GitHub-inspired features for code-sharing and collaboration, including discussions and pull requests for projects [2]. The company has multiple libraries for other tasks, such as dataset processing ("Datasets"), model evaluation ("Evaluate"), simulation ("Simulate"), machine learning demos ("Gradio")

Hugging Face offers a Python client library that allows users to programmatically access its platform features [1]. Users can use the Hub’s Python client library to take a first look at the Hub features [1]. Hugging Face Spaces is a hosted service that allows users to build web-based demos of machine learning apps using the Gradio or Streamlit

In February 2023, the company announced a partnership with Amazon Web Services (AWS) which would allow Hugging Face's products available to AWS customers to use them as the building blocks for their custom applications. The company also said the next generation of BLOOM will be run on Trainium, a proprietary machine learning chip created by AWS

## Building the frontend

I will create a frontend with Sveltekit and Tailwind CSS, and when I am done host an example on Vercel.

## References
[1] https://huggingface.co/docs/hub/overview
[2] https://en.wikipedia.org/wiki/Hugging_Face

Demo: https://gardenroute-mall-bot.vercel.app

This was only a quick overview of the project. Always feel free do contact me if you have any questions or if you want to collaborate on this project.