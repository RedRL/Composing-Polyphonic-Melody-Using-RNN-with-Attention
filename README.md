# 🎼 Composing Polyphonic Melody Using RNN with Attention

This project explores automatic generation of **polyphonic symbolic music** using recurrent neural networks enhanced with an attention mechanism.  
The system learns temporal and harmonic structure from musical sequences and generates coherent multi-voice continuations.

The focus of the project is not only next-step prediction accuracy, but also the **musical quality of generated sequences during free-running generation**.

---

## 📖 Overview

Automatic music generation is a challenging machine learning task because statistically plausible sequences may still sound repetitive or musically unstable.  
To address this, music is represented using a **piano-roll encoding**, where each time step is a binary vector over pitches and multiple notes may be active simultaneously.

The project is developed in three phases:

- **Phase 1 — Synthetic warm-up**  
  A simple harmonic environment is used to validate the full training and generation pipeline.

- **Phase 2 — Stacked LSTM baseline**  
  A recurrent model is trained on real chorale data to learn local temporal and harmonic structure.

- **Phase 3 — Attention-enhanced model**  
  An additive attention mechanism is introduced to improve contextual modeling and generation quality.

---

## 🎼 Dataset and Representation

The main experiments use the **JSB Chorales dataset**, converted into piano-roll sequences.

Key properties:

- Polyphonic binary encoding  
- Context window of 32 time steps  
- Fixed pitch-bin representation  
- Next-step prediction formulation  

This representation enables modeling harmonic combinations and temporal dependencies in symbolic music.

---

## 🧠 Model Architecture

### Phase 2 — Baseline
- 2-layer LSTM  
- Hidden size: 256  
- Dropout: 0.2  
- Fully connected prediction head  

This architecture captures meaningful **local musical structure**.

### Phase 3 — Attention Model
- Same recurrent backbone  
- Additive attention over hidden-state sequence  
- Context vector combined with recent representation  

Attention allows the model to focus on relevant past musical events when predicting the next frame.

---

## ⚙️ Training

Models are trained using:

- Binary next-frame prediction  
- BCEWithLogits loss  
- Adam optimizer  
- Early stopping based on validation loss  

Although the training objective is local, evaluation also considers **qualitative listening-based analysis**.

---

## 🎹 Generation Strategy

Music is generated autoregressively from a seed context.

Decoding includes:

- Temperature-controlled stochastic sampling  
- Polyphony constraints  
- Anti-freezing rules to encourage note turnover  

The project demonstrates that **decoding strategy significantly affects musical realism**, not only model architecture.

---

## 📊 Results

Both models learn meaningful harmonic structure.

**Baseline LSTM**
- Test loss: 0.076  
- F1 (micro): 0.8216  

**Attention Model**
- Test loss: 0.0722  
- F1 (micro): 0.8345  

The attention model achieves improved prediction performance and produces **more stable and musically usable continuations**.

---

## ⚠️ Limitations

- Piano-roll representation does not preserve voice identity  
- Training objective focuses on local prediction rather than global phrase structure  
- Frame-level metrics alone are insufficient for evaluating musical quality  

---

## ✅ Conclusion

This project presents an end-to-end pipeline for polyphonic music generation using recurrent neural networks with attention.  
Results show that attention provides measurable improvements, while final musical quality depends on the interaction between representation, decoding strategy, and evaluation methodology.

---

## 🛠 Technologies

- Python  
- PyTorch  
- NumPy / Matplotlib  
- PrettyMIDI / FluidSynth  
- Google Colab
