# Universal Language Model Fine-tuning for Text Classification Implementation

This project is a reproduction of the ["Universal Language Model Fine-tuning for Text Classification"](https://arxiv.org/abs/1801.06146) paper. The paper demonstrates that transfer learning (pre-training a language model on a large corpus and fine-tuning it for specific tasks) can be as effective in NLP as it has been in computer vision.

The data was scraped from the ["Rotten Tomato"](https://www.rottentomatoes.com/) website that can be found [here.](https://github.com/RezuwanHassan262/Universal-Language-Model-Fine-tuning-for-Text-Classification-Implementation/blob/main/data/film_details.csv)

Finally utilized Fast.AI's `text_classifier_learner` function and did discriminative supervised finetuned the ["Regularizing and Optimizing LSTM Language Models"](https://arxiv.org/abs/1708.02182) paper inspired  `AWD_LSTM` language model (Pre-trained LSTM model on Wikipedia Corpus) to classify text labels or genres. 

The paper "Universal Language Model Fine-tuning for Text Classification (ULMFiT)" by Jeremy Howard and Sebastian Ruder (2018) introduced a highly effective approach for text classification using pre-trained language models. The paper introduced a three-stage fine-tuning process that focuses on optimizing each stage for better transfer learning. The three stages progressively adapt the language model to the target task, ensuring the knowledge learned in earlier rounds is not overwritten. The ULMFiT authors argue that this sequential approach allows the model to leverage both general-domain knowledge and task-specific nuances.

The focus of the paper is on demonstrating the effectiveness of their three-stage framework rather than exploring whether additional rounds of fine-tuning (e.g., a "fourth stage") could yield further improvements but in practice, additional fine-tuning stages may lead to overfitting or diminished returns if not carefully regularized, as the model might overfit the small dataset for the target task. Which is shown below in the train-valid curve image. Note that I took the average learning rate in every stage of fine-tuning.

![four_stages_of_fnt](https://raw.githubusercontent.com/RezuwanHassan262/Universal-Language-Model-Fine-tuning-for-Text-Classification-Implementation/main/images/tt_curve.png)


To conclude, The ULMFiT paper revolutionized NLP by showing that pre-trained language models could be fine-tuned for a variety of downstream tasks with minimal labeled data. Its key innovations include the introduction of transfer learning techniques tailored for text, such as discriminative fine-tuning, slanted triangular learning rates, and staged training. The method not only outperformed traditional approaches but also demonstrated the universal applicability of pre-trained LMs, laying the foundation for subsequent advancements in NLP, such as BERT and GPT.

PS: It is noteworthy to mention that, I also played around by fine-tuning a few transformers architecture-based pre-trained base language models like Distilroberta, Alberta, Bert, and Xlnet.

