# Federated Learning Intrusion Detection System for the Internet of Things

**Master's thesis** · Academic year 2025/2026
University of Amar Telidji, Laghouat · Faculty of Sciences · Department of Computer Science
Field: Mathematics and Computer Science · Specialization: Networks, Distributed Systems and Applications

**Authors:** Yacine Chettouh, Mohammed Houssam Eddine Guenou
**Supervisor:** Dr. Youssra Cheriguene (MC(B))
**Jury:** Pr. Mustapha Bouakkaz (president) · Dr. Messaoud Babaghayou (examiner) · Dr. Laradj Chellama (examiner)

📄 **Read it:** [Yacine-Chettouh-Master-Thesis.pdf](Yacine-Chettouh-Master-Thesis.pdf) (GitHub renders the PDF in the browser; the download button is at the top right of the viewer)

---

## Abstract

Nowadays, the Internet of Things (IoT) is widely used across critical infrastructures, connecting
billions of embedded edge devices. In this context, securing these decentralized networks faces
significant limitations due to the severe resource constraints and privacy requirements of IoT
nodes, making traditional centralized Intrusion Detection Systems (IDS) impractical.

While Federated Learning (FL) offers a privacy-preserving alternative, standard protocols like
FedAvg face problems such as severe network congestion and high communication overhead caused by
the continuous transmission of massive, uncompressed model updates over low-bandwidth links. To
address these problems, this dissertation proposes a new communication-efficient Federated Learning
Intrusion Detection System (FL-IDS). Leveraging a FedProx optimization core, the framework
integrates an on-device Adaptive Gradient Quality Gate and top-k parameter sparsification to filter
redundant updates and drastically reduce payload sizes. Furthermore, an emergency staleness
override guarantees stable participation across the heterogeneous network.

The performance of the proposed architecture is analysed thoroughly and extensively through
simulation using the CICIoT2023 dataset. The results demonstrate that our framework achieves a
massive 80% reduction in cumulative communication bandwidth compared to standard FedAvg, while
successfully maintaining a high global detection accuracy of 91.5% and a macro F1-score of 0.786.
Hence, this work provides a significant improvement in IoT security protocols, presenting a
reliable, resource-aware solution for modern edge environments while establishing a basis for
future research in the field.

*(The thesis also contains the Arabic version of this abstract.)*

## Results

Evaluation: CICIoT2023 consolidated into four classes (Benign, DoS, Mirai, Other), ten non-IID
clients, 50 federated rounds, top-k sparsification with k = 0.2, quality threshold τ_Q = 0.35.

| Metric | FedAvg (baseline) | FL-IDS (this work) |
| --- | --- | --- |
| Cumulative uplink traffic, 50 rounds | 100 % | **20 %** (80 % reduction) |
| Global accuracy | — | **91.5 %** |
| Macro F1-score | — | **0.786** |
| Convergence | — | stable across 50 rounds |

Three components carry the result, all on the client side except the aggregation:

1. **Adaptive Gradient Quality Gate** — each client measures the quality of its own update before
   transmitting and drops it when it would degrade the global model; the threshold starts permissive
   (warmup) and saturates as the model learns.
2. **Emergency Staleness Override** — a client that has been silent too long is allowed to transmit
   regardless of the gate, so slow-but-honest devices are not starved out of the federation.
3. **Top-k sparsification + quality-weighted aggregation** — only the largest gradient components
   are sent, and the server weights each contribution by its reported quality.

An ablation study over the three components confirms that each one contributes, and that the
quality gate is what protects accuracy when the traffic is cut.

## How to read it

The PDF opens in GitHub's viewer; use **Download** at the top right to save it.

If you only have ten minutes:

- **Chapter 1 — General Introduction:** the problem and the research question.
- **Chapter 4 — Our Contribution:** the architecture in five figures (system model, quality gate,
  staleness override, top-k selection, per-device flow).
- **Chapter 5 — Results and Discussion:** convergence, per-class F1, FedAvg comparison, ablation.

The full document follows the classic structure: background (2), related work with a comparison
table of FL-based IDSs (3), contribution and implementation (4), results (5), conclusion and future
work (6).

## Implementation

The framework was implemented as a reproducible **pure PyTorch** codebase (no FL framework): a
modular layout with separate client, server, gating, sparsification and evaluation modules, a
preprocessing pipeline for CICIoT2023, and a compact multilayer perceptron (`IDSModel`) as the
detector.

## Citation

```bibtex
@mastersthesis{chettouh2026flids,
  title  = {Federated Learning Intrusion Detection System for the Internet of Things},
  author = {Chettouh, Yacine and Guenou, Mohammed Houssam Eddine},
  school = {University of Amar Telidji, Laghouat},
  year   = {2026},
  type   = {Master's thesis},
  note   = {Supervisor: Dr. Youssra Cheriguene}
}
```

---

🌐 Portfolio: **[chettouhyacine.github.io](https://chettouhyacine.github.io/)** · 📫 chettouhyacine2001@gmail.com
