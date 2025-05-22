# Prompt Iterations

Due to the issues laid out in section 3 of the thesis, he prompt adopted from Scire et al. (2024) went through three major iterations (v1 - v3):

- **v1: Appending a definition of "core claims"**  
  Adding instructions to limit the number of extracted claims to a maximum of five and to only include claims that can be considered core claims.

- **v2: Changing the original example input-output pair**  
  Modifying it to be a news article and its respective core claims. Adding further instructions to obtain information on whether a claim was made in the headline and to specify the token position of where a claim was made in the original article alongside the total token count.

- **Assigning an ID to each sentence in an article**  
  Amending the instructions to ask for the sentence ID instead of the token position. Ensuring the JSON format is correctly structured.

---

The main purpose of the first version, building on the original prompt provided by Scire et al. 2024, was to limit the number of claims the LLM would return. Given that the original definition led to numerous and rather granular claims being extracted during prior experiments, it was modified to explicitly mention "core claims." Additionally, the prompt was expanded with an instruction asking the model to extract only five claims, ensuring they met the "core" criteria according to the provided definition.

The second version further tailored the prompt to the specific use case of this thesis by changing the example input-output pair to a news article and its respective claims in the desired format. Furthermore, additional instructions were introduced to obtain data relevant for the score's calculation, including a binary indicator of whether a claim appeared in the headline and its position within the article. The instructions initially asked the model to return the position of the token where a claim started. However, this approach led to evident instances of hallucinations, with the model failing to refer to accurate token positions.

To address this issue, the third and final version assigned a unique identifier to each sentence within an article, a method proven to limit hallucinations in LLMs Felman et al. (2023). Consequently, the example included in the prompt was pre-processed accordingly, following the procedure outlined in the thesis. Naturally, the instructions were adjusted to request the first sentence ID instead of the position of the first token. These changes resulted in noticeable improvements in retrieval accuracy, with the model consistently identifying the correct sentence in random samples. However, during claim processing, it became apparent that the model frequently failed to adhere to the JSON format, specifically causing missing or incorrect braces and brackets in twelve out of seventeen fake or misleading articles in the Aslett et al. dataset. This issue was successfully addressed by explicitly instructing the model to pay attention to proper formatting, leading to seventeen correctly formatted results.
