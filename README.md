# Reverse-Engineered-Gemma-2B
An Investigation into Layer Interactions : Gemma 2 2b Finding a feature that activates on famous married couples

Introduction: 
The first time I developed curiosity to learn and apply knowledge of mechanistic interpretability was when I watched Neel Nanda’s detailed tutorials on transformers. This led me to dive deeper into other concepts which focused on reverse engineering of LLM.  
After understanding the given research articles, my thirst towards understanding GPT models and superposition increased.  
Therefore, when I explored and played around the interactive demo of Gemmascope, a research question arose: Is there any interesting feature working across different layers of the Gemma 2 2b model? 
Since finding features is a labour intensive task, I believe investigating this research question might help to interpret the working of Gemma 2 2b contributing to the alignment research. 

Approach:  
In this exploration, I delved into how different layers within the Gemma model interact with each other and investigated if there is any internal communication or feature sharing across layers. By rigorously searching and analysing features across various layers and inputs, I identified specific features, such as those associated with personal relationships (e.g., "Lady Melania Trump is the wife of the 45th President, Donald J. Trump"). After isolating features that activate on the same topic and index location, I hypothesised that features of personal relationships such as marriage and name of famous individuals could be found in multiple layers because these concepts are likely reinforced and refined as the model processes information. This suggests that the model may have developed a hierarchical understanding of such features (Marks et al., 2024). 
To progress, I conducted an in-depth analysis of how these features behaved in response to different inputs, including token position changes. 
I further tried to explore how the model could be steered using these features and tested the model's resilience to incorrect or misleading inputs, a process known as red-teaming.

Summary of key findings: 
The following google Collab link: https://colab.research.google.com/drive/1n9tOKx5ZBC78iv2ylGOW7IMyV-BT8yGt?usp=sharing explains my progress. 

Here I highlight key findings and progress on the topic: 
Image 1: The "happy face lol feature" could refer to a feature in a model that detects or interprets emoticons like ":)" as expressions of happiness or positivity. 

While exploring the interactive demo, I observed many features. Some were common and easy to understand. My aim was to find feature circuits, so I started searching related features on different layers (Marks et al., 2024). I found some of them but the activation score of those features was very low. Thus, following Neel Nanda's suggestion to examine the case studies of feature splitting in the layer 12 SAEs of Gemma 2 2b . 



After exploring layer 12 we can easily see that these are mature features compared to previous layers. Onward the rigorous tests of different inputs and concepts led to discovery of the feature “references to personal relationships and family connections” of Index-969. Then I tested the same input through all 26 layers in search of similar features.

Eureka!! I found a similar feature “references to women and their relationships, particularly focusing on familial ties and accomplishments” on layer 11 on the same Index-969 position. Yes I know it's strange and unimaginable but it's there. 
However, analysing this feature layer wise with different input and positions does not give me results as hypothesised. To tackle this, I did the “Contrast Pairs Trick” by swapping the word “marriage” with “divorce” (Classic example of red-teaming).  As seen in image 3 , the generated output includes false and potentially harmful information. The output falsely claims that Angela Merkel’s husband, Joachim Sauer, died and provides fabricated details about the circumstances.

For a deeper understanding of these features I decided to do feature steering. While doing that I encountered code error for retrieving weights of layer 11 and 12 SAE’s. While debugging I thought to try steering with red-teaming on input. Lacking a time constraint , I tried random weights for feature steering. As a result, it gave me satisfactory outcomes as shown in image 4. Also the scaling factor coefficient value shows direct proportion to ambiguity in output generation of the model. On researching different combinations we see that the model gives false claims with a link to news article.
