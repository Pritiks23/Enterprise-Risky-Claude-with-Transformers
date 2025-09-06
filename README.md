# Enterprise-Risky-Claude-with-Transformers


<img src="https://github.com/user-attachments/assets/7b88ef99-c3f1-44b4-ae3e-ddd1af0117d0" width="300" />

<img src="https://github.com/user-attachments/assets/508efbbb-7e46-4810-af46-4dc453e3f94c" width="300" />




# Technical Overview

This project implements a transformer-based Question Answering (QA) system specialized for legal contract analysis. At its core, it uses a fine-tuned DistilBERT model, a distilled variant of BERT optimized for reduced memory footprint and faster inference while retaining most of BERT’s representational power. The system is designed to automatically identify and extract risk-related clauses from contracts, such as auto-renewal, late payment penalties, early termination, indemnification, confidentiality, data privacy, intellectual property, and exclusivity. By leveraging the contextual embeddings produced by the transformer layers, the model captures the semantic relationships between questions and context, allowing it to locate clauses even when phrased variably across different contracts.

Training data consists of contract contexts paired with specific questions, with answers labeled as exact character spans in the text. During preprocessing, both the question and the context are tokenized together into subword tokens using DistilBERT’s tokenizer. An offset mapping is generated to align the original character positions of the answer with the corresponding token indices. This alignment ensures that the start and end token indices used during training accurately correspond to the true span of the answer in the text, which is essential for precise extraction of legal clauses. Without this alignment, the model could learn misaligned token positions, reducing extraction accuracy.

The model is fine-tuned using a token-level cross-entropy loss function applied separately to the start and end token logits, allowing the network to learn to predict the exact token boundaries of an answer span. Input sequences are padded and truncated to a fixed maximum length to comply with the transformer architecture, and attention masks are applied to prevent the model from attending to padded tokens. Through this mechanism, DistilBERT’s self-attention layers effectively model long-range dependencies within the contract text, capturing the contextual meaning of clauses relative to the posed question, even in cases where key terms are separated by intervening text.

Once fine-tuned, the model can be deployed to automatically extract clauses from new contracts. The output includes both the predicted text span and a confidence score derived from the softmax probabilities of the start and end token predictions. By combining subword-level tokenization, offset mapping, and transformer-based contextual embeddings, the system enables highly accurate, scalable, and interpretable extraction of legally significant terms. This approach significantly reduces the manual effort required for contract review and supports automated analysis of large volumes of contracts while maintaining precision in capturing risk-relevant information.

## CHECK IT OUT FOR YOURSELF: https://colab.research.google.com/drive/1pmq46xWcxKKsh9nhX9irJhM_34Qd8o-O?usp=sharing
