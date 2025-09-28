## Goal : VLA models , commoditizing robotics 


Start with the basics: 


[✔️] Transformers  
[✔️] ViT models  
[✔️] CLIP model   
[✔️] SigLIP model  
[] Pixel Shuffle  
[] VLM model (SmolVLM papers)  
[] VLA model   



## Vision Transformer : 
Transformers backbone with patches embedding with positional embedding , a feature extractor backbone !


## CLIP : 
Trained on Image-caption pairs (Image - Caption (IMG, Caption)), so the text encoder and the image encoder , so we can get an idea of text just by looking at the iamge embeddings so its learned image features, with additional text feature extractor ( matcher ) ! 


## Pixel shuffling 

Upscaling operation , not done by pure maths , but using neural nets which are again pure maths ( if u understand this black box ) , so basically here we are trying to learn to optimally upscale the images

This also helps to reduce the no. of visual tokens , required / compresses the visual tokens  

## VLM model (SmolVLM)

Here we input both the images along with the text question that we have so it requires an extractor that is trained on both the images and as well as text and learned joined embedding , so here we have to use the VLM model 
paper link : https://arxiv.org/pdf/2504.05299 



## Flow matching 
> TODO : Why to use diffusion or flow matching to generation action tokens ? 



## SmolVLA model 

Here the input is the (text/ language instructions + images + action state) to the the VLM model (discarding the last L-N layers ) , the model on top adds a head to find the relevant action for these images so the input is the observation and output is the action state and this happens. Action expert, takes in merged token embedding consist of alternating cross attention layers and self attention layers and this outputs a chunk of low level actions using flow matching .. 


## OpenVLA model 

Here also we use VLM and all the innovation is in using the action tokenizer model, the LLM is finetuned to perform a different task that is to output action tokens( the VLM is trained to output action tokens) these action token ids are passed as input to the action tokenizer. 

So the delta is learning the action expert / tokenizer and improving the model / paper ! 
The moat is in the way of how we learn / modify the action states !

## Pi0 fast model 

Action tokenizer, to normalise action to -1 to 1, then uses Discrete cosine transform (DCT) per dimension to convert time domain action chunks into freq. domain. Removes insignificant freq. coefficients then applies BPE to map discrete token vocab. 

Refer to this colab notebook for more xplanation : 
https://colab.research.google.com/drive/1DPoaogAInKA9b5rxCiZoB1BC-fJ1rI-U?usp=sharing 

So, the current MOAT in late 2025 for robo companies is the Action tokenizer 


## FAST action tokenizer 
This uses DCT to compress, https://www.physicalintelligence.company/research/fast 
then quantises 

but its still much slower than the flow matching approach 


## DCT for signal compression 

https://www.youtube.com/watch?v=Kv1Hiv3ox8I

Here’s the live DCT-based compression of your signal:

Original signal:
[10, 12, 15, 20, 18, 16, 14, 12, 11, 13, 17, 19, 21, 20, 18, 15]

DCT coefficients:
[62.75, -5.88, 2.24, -2.76, -11.29, 0.33, -1.10, 0.30, 0.25, 1.72, 0.67, -0.16, -0.47, -0.41, -1.25, -0.14]

Compressed coefficients (keeping top 30% energy):
[62.75, -5.88, 2.24, -2.76, -11.29, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]

Reconstructed signal:
[9.78, 12.21, 15.73, 18.38, 18.76, 16.76, 13.65, 11.30, 11.14, 13.35, 16.78, 19.68, 20.68, 19.58, 17.43, 15.78]

Compression ratio:
3.2x (original 16 non-zero coefficients → 5 stored coefficients)

The signal is approximated well with only a fraction of the coefficients.

then Quantize to integers and then make use BPE to club tokens ( byte pair encoding )


Training fast but the inference is Slow

