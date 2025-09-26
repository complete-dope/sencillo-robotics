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



## VLA model (SmolVLA) / ( lerobot )

Here the input is the (text/ language instructions + images + action state) to the the VLM model (discarding the last L-N layers ) , the model on top adds a head to find the relevant action for these images so the input is the observation and output is the action state and this happens. Action expert, takes in merged token embedding consist of alternating cross attention layers and self attention layers and this outputs a chunk of low level actions using flow matching .. 


