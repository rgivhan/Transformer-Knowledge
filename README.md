# Transformer-Knowledge

We test the performance of Kaparthy's minGPT Transformer model on a simple knowledge task.

First we pretrain minGPT on Wikipedia text about notable individuals, then we finetune it on name-birthplace pairs of the form: 

Q: Where was [person] born?
A: [place]

We then test its "knowledge" by asking it to predict the birthplaces of individuals in the same question answer format as above. 

# Attention

Two variants of self attention are tested: standard Masked multi-headed self-attention, and Synthesizer attention. The model using Masked multi-headed self-attention achieves an accuracy of ~20%. The model using the synthesizer variant, which is a form of attention that eschews the use of pairwise dot products, achieves ~17% accuracy. 



# Pretraining

For specifics, see the CharCorruptionDataset class in dataset.py. To pretrain on the wikipedia text, a piece of text is randomly truncrated and masked. For every such piece of text, $x$, its label, $y$ is truncated by a single character at the beginning (i.e. $y = x[1:]$), such that, for each character, the model is trying to preidct the next character in the masked string $x$

I.e.\
__Original__: Khatchig Mouradian. Khatchig Mouradian is a journalist, writer and translator born in Lebanon .\
__x__: Khatchig Mouradian. Khatchig Mouradian is a jour⁇and tran⁇nalist, writer ⁇□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□\
__y__: hatchig Mouradian. Khatchig Mouradian is a jour⁇and tran⁇nalist, writer ⁇□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□□


