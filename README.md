# Attention
 AI to predict a masked word in a text sequence using Google BERT Masked Language Model from Hugging Face Transformers

•	AI to predict a masked word in a text sequence using Google Bidirectional Encoder Representations from Transformers (BERT) Masked Language Model from Hugging Face Transformers library and generate diagrams visualizing attention scores for each of the 144 self-attention heads for a given sentence.

•	Used TensorFlow to get top k predicted tokens from vocabulary logits for mask token from the input sequence


<img width="1042" alt="image" src="https://github.com/user-attachments/assets/cfdc73bc-509e-498d-8e7e-04ec12d8ddc1" />

These diagrams can give us some insight into what BERT has learned to pay attention to when trying to make sense of language. Below is the attention diagram for Layer 3, Head 10 when processing the sentence “Then I picked up a [MASK] from the table.”

## Layer 3, Head 10

<img width="678" alt="image" src="https://github.com/user-attachments/assets/3cdae797-09cf-4d5d-850e-90b6455f8e83" />

Lighter colors represent higher attention weight and darker colors represent lower attention weight. In this case, this attention head appears to have learned a very clear pattern: each word is paying attention to the word that immediately follows it. The word “then”, for example, is represented by the second row of the diagram, and in that row the brightest cell is the cell corresponding to the “i” column, suggesting that the word “then” is attending strongly to the word “i”. The same holds true for the other tokens in the sentence.

I was curious to know if BERT pays attention to the role of adverbs. I gave the model a sentence like “The turtle moved slowly across the [MASK].” and then looked at the resulting attention heads to see if the language model seems to notice that “slowly” is an adverb modifying the word “moved”. Looking at the resulting attention diagrams, one that catched my eye was Layer 4, Head 11.

## Layer 4, Head 11

<img width="597" alt="image" src="https://github.com/user-attachments/assets/36ed06e2-5b47-450e-b0ae-8451dfa5a2b0" />

This attention head is definitely noisier: it’s not immediately obvious exactly what this attention head is doing. But notice that, for the adverb “slowly”, it attends most to the verb it modifies: “moved”. The same is true if we swap the order of verb and adverb.

<img width="599" alt="image" src="https://github.com/user-attachments/assets/e808ce0c-6091-43dc-8df1-dad7a02506a4" />

And it even appears to be true for a sentence where the adverb and the verb it modifies aren’t directly next to each other.

<img width="519" alt="image" src="https://github.com/user-attachments/assets/5fd3c577-3409-4ef9-9ca2-2caa8566a552" />

## Layer 8, Head 5

This head shows a diagonal pattern where tokens are paying attention to the tokens that precede them in the input sequence.

Example Sentences:
- I threw a small rock and it fell in the [MASK].

  ![Attention_Layer8_Head5](https://github.com/user-attachments/assets/70babaa2-24af-4acc-816d-18058dd7b409)



- I was walking with my dog [MASK] it started barking.

  ![Attention_Layer8_Head5](https://github.com/user-attachments/assets/dc153d91-4e52-4394-b634-68206d46be2a)


  

## Layer 9, Head 11

This head focuses primarily on the SEP token, with the pronoun "it" paying attention to the object it is referring to , i.e. "rock" in the 1st sentence and "dog" in the 2nd sentence.

Example Sentences:
- I threw a small rock and it fell in the [MASK].

  ![Attention_Layer9_Head11](https://github.com/user-attachments/assets/91a49e84-7b2e-4001-9682-cb9826ec6209)

- I was walking with my dog [MASK] it started barking.

  ![Attention_Layer9_Head11](https://github.com/user-attachments/assets/849ea290-5bb8-4ca2-8bfc-77596ad069a2)




