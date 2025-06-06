# Scalable mRNA sequence design under biological constraints

Code repository and notebooks for paper titled: "Scalable mRNA sequence design under biological constraints"

We trained an unsupervised codon-level language model (codonLLM) to learn contextual dependencies within protein-coding sequences across the human genome. To construct the training corpus, we extracted annotated coding sequences (CDS) from Ensembl and segmented each into triplet codons. We used a custom tokenizer designed for the biological codon vocabulary, consisting of 64 standard codons and three special tokens: [PAD], [BOS], and [EOS]. Each sequence was tokenized as a flat sequence of codons, without any alignment to amino acid sequences, enabling the model to learn the intrinsic distributional properties of codon usage independent of protein identity.

The model architecture was based on a GPT-2-like decoder-only transformer. It was trained in an autoregressive fashion using the standard next-token prediction objective, optimizing cross-entropy loss. Pretraining was conducted using batches of randomly sampled CDS regions, ensuring coverage across diverse expression levels and gene categories. 

This pretraining phase resulted in a codonGPT capable of capturing long-range dependencies and codon co-occurrence patterns within coding regions, including biologically relevant motifs and synonymous codon bias. The pretrained model serves as a foundation for downstream tasks such as organism-specific codon optimization, sequence generation, and biological constraint-aware fine-tuning using reinforcement learning.

The model is available at https://huggingface.co/naniltx/codonGPT 

In this github repo, we provide 3 notebooks that demonstrate use of the model 

- evaluation with HKG
- evaluation with 100 sampled sequences
- a mRNA sequence design framework using Reinforcement learning
