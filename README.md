# Universal Language Model Fine-tuning for Text Classification Implementation

This project is a reproduction of the ["Universal Language Model Fine-tuning for Text Classification"](https://arxiv.org/abs/1801.06146) paper. The paper demonstrates that transfer learning (pre-training a language model on a large corpus and fine-tuning it for specific tasks) can be as effective in NLP as it has been in computer vision.

The data was scraped from the ["Rotten Tomato"](https://www.rottentomatoes.com/) website and is available [here.](https://github.com/RezuwanHassan262/Universal-Language-Model-Fine-tuning-for-Text-Classification-Implementation/blob/main/data/film_details.csv)

Finally utilized Fast.AI's `text_classifier_learner` function and did discriminative supervised finetuned the ["Regularizing and Optimizing LSTM Language Models"](https://arxiv.org/abs/1708.02182) paper inspired  `AWD_LSTM` language model (Pre-trained LSTM model on Wikipedia Corpus) to classify text labels or genres. 

The paper "Universal Language Model Fine-tuning for Text Classification (ULMFiT)" by Jeremy Howard and Sebastian Ruder (2018) introduced a highly effective approach for text classification using pre-trained language models. The paper introduced a three-stage fine-tuning process that focuses on optimizing each stage for better transfer learning. The three stages progressively adapt the language model to the target task, ensuring the knowledge learned in earlier rounds is not overwritten. The ULMFiT authors argue that this sequential approach allows the model to leverage both general-domain knowledge and task-specific nuances.

The focus of the paper is on demonstrating the effectiveness of their three-stage framework rather than exploring whether additional rounds of fine-tuning (e.g., a "fourth stage") could yield further improvements but in practice, additional fine-tuning stages may lead to overfitting or diminished returns if not carefully regularized, as the model might overfit the small dataset for the target task. Which is shown below in the train-valid curve image. Note that I took the average learning rate in every stage of fine-tuning.

<div align="center">
  <img src="https://raw.githubusercontent.com/RezuwanHassan262/Universal-Language-Model-Fine-tuning-for-Text-Classification-Implementation/main/images/tt_curve.png" alt="Four stages of the finetuning train-valid curve">
</div>

The training parameter of the third stage and the training progress and metrics.

    Suggested learning rate (slide): 0.0006918309954926372
    Suggested learning rate (valley): 3.630780702224001e-05
    Average learning rate: 0.0003640694012574386
    Suggested ALR: 0.36e-3

`learner.fit_one_cycle(n_epoch = 100, lr_max = slice(lr_min, lr_steep), cbs=EarlyStoppingCallback(monitor='accuracy', min_delta=0.1, patience=10)) #Takign the average of suggested slide and valley`

| Epoch | Train Loss | Valid Loss | Accuracy | Perplexity | Time |
|---|---|---|---|---|---|
| 0 | 0.532324 | 0.502562 | 0.857191 | 1.652951 | 00:27 |
| 1 | 0.549340 | 0.494193 | 0.859543 | 1.639174 | 00:28 |
| 2 | 0.543409 | 0.494593 | 0.862567 | 1.639831 | 00:28 |
| 3 | 0.564304 | 0.492928 | 0.860887 | 1.637103 | 00:29 |
| 4 | 0.537835 | 0.489772 | 0.861559 | 1.631944 | 00:28 |
| 5 | 0.496488 | 0.493346 | 0.859879 | 1.637787 | 00:28 |
| 6 | 0.526380 | 0.492810 | 0.859543 | 1.636909 | 00:28 |
| 7 | 0.514410 | 0.487982 | 0.861223 | 1.629026 | 00:28 |
| 8 | 0.536183 | 0.489782 | 0.862231 | 1.631960 | 00:28 |
| 9 | 0.475815 | 0.488019 | 0.862231 | 1.629086 | 00:29 |
| 10 | 0.464559 | 0.489713 | 0.859543 | 1.631849 | 00:27 |

`No improvement since epoch 6: early stopping`

To conclude, The ULMFiT paper revolutionized NLP by showing that pre-trained language models could be fine-tuned for a variety of downstream tasks with minimal labeled data. Its key innovations include the introduction of transfer learning techniques tailored for text, such as discriminative fine-tuning, slanted triangular learning rates, and staged training. The method not only outperformed traditional approaches but also demonstrated the universal applicability of pre-trained LMs, laying the foundation for subsequent advancements in NLP, such as BERT and GPT.

PS: It is noteworthy to mention that, I also played around by fine-tuning a few transformers architecture-based pre-trained base language models like Distilroberta, Alberta, Bert, and Xlnet.

