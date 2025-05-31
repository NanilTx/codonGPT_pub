# codonGPT_pub

Code repository and notebooks for paper titled: "Scalable mRNA sequence design under biological constraints"

We trained an unsupervised codon-level language model (codonLLM) to learn contextual dependencies within protein-coding sequences across the human genome. To construct the training corpus, we extracted annotated coding sequences (CDS) from Ensembl and segmented each into triplet codons. We used a custom tokenizer designed for the biological codon vocabulary, consisting of 64 standard codons and three special tokens: [PAD], [BOS], and [EOS]. Each sequence was tokenized as a flat sequence of codons, without any alignment to amino acid sequences, enabling the model to learn the intrinsic distributional properties of codon usage independent of protein identity.

The model architecture was based on a GPT-2-like decoder-only transformer with a maximum sequence length of 1024 codons. It was trained in an autoregressive fashion using the standard next-token prediction objective, optimizing cross-entropy loss. Pretraining was conducted using batches of randomly sampled CDS regions, ensuring coverage across diverse expression levels and gene categories. We used the Adam optimizer with linear learning rate warmup followed by cosine decay. Regularization included dropout on attention and feed-forward layers, as well as gradient clipping. The model was trained until convergence on a compute cluster with multiple A100 GPUs, with validation loss used to monitor overfitting.

This pretraining phase resulted in a codonLLM capable of capturing long-range dependencies and codon co-occurrence patterns within coding regions, including biologically relevant motifs and synonymous codon bias. The pretrained model serves as a foundation for downstream tasks such as organism-specific codon optimization, sequence generation, and biological constraint-aware fine-tuning using reinforcement learning.

We provide 3 notebooks. 

- evaluation with HKG
- evaluation with 100 sampled sequences
- a mRNA sequence design framework using Reinforcement learning
