# Canada Quant Labs

Canada's open-weight model lab.

We train, quantize, and deploy sovereign AI models on Canadian Blackwell silicon — for the regulated industries that can't run on someone else's API.

**What we do**
- Post-training on open base models (SFT, DPO, GRPO, RLAIF)
- Production quantization recipes (W4A16, NVFP4, MXFP4)
- Audited, air-gapped deployment with eval evidence and MRM docs

**Where we work**
- Legal · Medical · Defence · Finance
- Headquarters: Victoria, BC
- Compute: NVIDIA DGX B300 at Equinix Vancouver

**Upstream**
- Contributors to vLLM, llm-compressor

Partnerships · partnerships@cql.ca
Press · press@cql.ca
Web · cql.ca

---

## Open releases — DeepSeek-V4 quantization family

Four artifacts in the same lineage. One base model in two sizes (V4-Flash, V4-Pro); two routed-expert formats (W4A16, NVFP4); MTP draft head retained on three of four. Attention is FP8 block 128×128 across all four. Upstream reference recipes: [`RedHatAI/DeepSeek-V4-Flash-NVFP4-FP8`](https://huggingface.co/RedHatAI/DeepSeek-V4-Flash-NVFP4-FP8) (Flash NVFP4) and [`nvidia/DeepSeek-V3.2-NVFP4`](https://huggingface.co/nvidia/DeepSeek-V3.2-NVFP4) (Pro NVFP4, MTP-exclusion topology).

| Repo | Base | Routed experts | MTP | On-disk | Min hardware (TP=2) | When to pick |
|---|---|---|---|---|---|---|
| [W4A16-FP8](https://huggingface.co/canada-quant/DeepSeek-V4-Flash-W4A16-FP8) · [src](https://github.com/canada-quant/dsv4-flash-w4a16-fp8) | V4-Flash | W4A16 INT4 g=128 | no | ~143 GB | H200 / DGX Spark / RTX PRO 6000 | maximum compatibility, no MTP needed |
| [W4A16-FP8-MTP](https://huggingface.co/canada-quant/DeepSeek-V4-Flash-W4A16-FP8-MTP) · [src](https://github.com/canada-quant/dsv4-flash-w4a16-fp8-mtp) | V4-Flash | W4A16 INT4 g=128 | yes (BF16) | 159 GB | H200 / RTX PRO 6000 | best $/token interactive on V4-Flash |
| [NVFP4-FP8-MTP](https://huggingface.co/canada-quant/DeepSeek-V4-Flash-NVFP4-FP8-MTP) · [src](https://github.com/canada-quant/dsv4-flash-nvfp4-fp8-mtp) | V4-Flash | NVFP4 g=16 | yes (BF16) | 172 GB | RTX PRO 6000 / B300 | best Blackwell-native interactive on V4-Flash |
| [Pro NVFP4-FP8-MTP](https://huggingface.co/canada-quant/DeepSeek-V4-Pro-NVFP4-FP8-MTP) · [src](https://github.com/canada-quant/dsv4-pro-nvfp4-fp8-mtp) | V4-Pro | NVFP4 g=16 | yes (byte-identical) | 913 GiB | 8× B300 (TP=8 + EP) | only choice for V4-Pro deployment; +25-37% throughput vs upstream MXFP4 |

Hardware shorthand: **H200** = 8× NVIDIA H200 SXM5 (Hopper SM 9.0a, 141 GB HBM3e/GPU). **DGX Spark** = 2× NVIDIA DGX Spark (GB10, Blackwell SM 12.1a). **RTX PRO 6000** = NVIDIA RTX PRO 6000 Blackwell Server Edition (SM 12.0, sm_120, 96 GB HBM). **B300** = NVIDIA B300 SXM6 AC (Blackwell SM 10.3, sm_103a, 288 GB HBM3e/GPU).
