# Tokenizer

> "Tokenization is at the heart of much weirdness of LLMs. Do not brush it off." - Andrej Karpathy

A tokenizer translates back and forth between strings and sequences of symbols from a codebook. This is a fundamental preprocessing step that converts raw text into tokens (integers) that language models can process.

## 1. Train the tokenizer
By default we are training a vocab size of 2**16 = 65,536 tokens (a nice number), of which a few tokens are reserved as special (to be used for the chat schema later). The training set is 2B characters, which only takes ~1 minute. The training algorithm is identical to the one used by OpenAI (regex splitting, byte-level BPE).

###BPE (byte pairing enconding algorithm) as mechanism for tokenization
From GPT-2 paper:
Vocabulary of 50,257 tokens.
Context size of 1024 tokens.
So in the attention layer every token is appending to the sequence of previous tokens, and is going to see up to 1024 tokens.

Tokenizer is needed to go from text to sequences to tokens, and viceversa.

###Why do you need tokenization?
Spell words problems? tokenization
Bad at simple arithmetic? Tokenization
worse at non-english languages? Tokenizaton
Use yaml instead of json? Tokenization

In english it will create fewer tokens, but in other laguages, it is going to create more tokens for the same text, this has to do with the tokenization.
GPT-2 is not good with python, because if you use a lot of indetation, I will consume a lot of tokens, so it will blow up the context length (not because of the model, but because of the tokenizer).

In gpt-4 the same text is squished in half of the tokens, so it is less dense input in the transformer. In the transformer is able to see twice as much token to generate the next token.
But if you increase the number of the tokens, the embedding table is going to be the double (gpt2= 50k, gpt4=100k), and also the output is going to predict the next token, and there is the softmax there.

There is an appropriate number of tokens for your vocabulary, where everything is properly dense, and still fairly efficient.

In gpt-4 they decided to optimize the tokenizer for python, in this way they can see more code before, predicting the next token (python code).
So from gpt-2 to gpt-4 the improvements comes a lot also from tokenizer.