# Community Image Lab — Colab integration for Qwen-Image-2.1

**Built with Qwen · 非官方社区整合 / Unofficial community integration**

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/PinKoalaXu/Qwen_Image_2_1_Ultimate_Uncensored_Colab/blob/main/Qwen_Image_2_1_Ultimate_Uncensored_Colab.ipynb)

[中文公告](#中文公告) · [English announcement](#english-announcement) · [组件与授权 / Components and licensing](#components-and-licensing) · [法律与版权 / Legal and copyright](#legal-and-copyright)

## 中文公告

这是由 **PinKoalaXu** 整理的 Google Colab 运行笔记本，以 **Qwen-Image-2.1** 为基础，将社区模型、VAE、多模态文本编码器和 5 款 LoRA 的下载、加载、调参与图像生成/编辑流程集中到同一份笔记本，减少手动搭建环境的步骤。本项目贡献的是部署与交互流程整合；基座及各社区组件均归其原作者所有。

笔记本默认选择 ChatR Labs Uncensored Omni 的 Step 90000 BF16 合并 Transformer，并提供官方原版与 Turbo 选项；可切换 Texture-Fix VAE 和 Heretic 文本编码器，通过 Gradio 调节 5 款 LoRA，进行文生图、参考图编辑及最多 10 张参考图的输入，并导出高质量 JPG。另附 Colab 原生上传/下载的单图编辑流程。

代码包含 LoRA 键名及融合层转换、True CFG 负面提示词处理、按显存选择 GPU 常驻/CPU offload、VAE tiling 策略及 JPG 导出设置。它们是实现中的兼容性处理，不构成“全部 Bug 已修复”、所有硬件可用或输出质量的保证。

**授权提醒：Qwen-Image-2.1 和 Turbo 当前采用 Qwen Research License，而非允许任意商用的宽松开源许可证。其授权范围仅限非商业研究或评估，商业用途须向上游取得单独许可。** 可公开下载不等于可自由商用；每个社区组件还须分别核对授权。请先阅读下方法律与版权说明及上游原文。

**欢迎公众共同完善：** 欢迎通过 Fork → 修改 → Pull Request 贡献代码、修复、运行记录、文档和翻译，也欢迎在 Issues / Discussions 提出建议。修改由维护者审核后合并。请先阅读 [贡献指南](CONTRIBUTING.md)，清除输出与个人信息，并保留全部上游许可和署名。

### 开始使用

1. 点击上方 **Open in Colab**，选择 GPU 运行时，先阅读所有单元内容。
2. 依次运行 **1 → 2 → 3 → 3B**，完成 GPU 检查、依赖安装、基座及 LoRA 加载。
3. 选择 **4A** 上传参考图并直接下载 JPG，或选择 **4B** 启动 Gradio 工作台。
4. 按实际显存、系统内存和存储空间调整组件与分辨率。完整 BF16 组件需要大量资源，免费 Colab GPU 不保证可运行；Colab 配额、断线及费用由 Google 决定。

本项目提供集中式 Colab 运行入口，首次使用仍需分配 GPU、下载权重并按顺序执行单元。Turbo 与社区 LoRA 的组合需要单独验证。

### 运行状态与隐私

- 发布前检查了 JSON 结构及 6 个代码单元的 Python 语法（Colab shell 指令单独处理）；未进行 GPU 端到端推理验证。依赖及模型均未固定 revision，上游更新可能影响兼容性。
- 发布文件未发现个人邮箱、个人目录、常见访问令牌/API key、IP 地址、单元输出或内嵌附件。该结果针对本次文件静态检查，不是对未来运行内容的保证。
- **4B 默认执行 `demo.launch(share=True, debug=True)`，会创建公开的 Gradio 临时分享链接，而且没有配置身份验证。持有链接的人可能访问界面、提交任务并查看界面暴露的数据。请勿上传私密资料或公开转发链接；使用后终止会话。** 调试输出和日志也应在分享前检查。
- 运行时会连接 Google Colab、Hugging Face、GitHub、Python 包下载服务及 Gradio 分享服务。请遵守相应服务条款与隐私政策。不要把访问令牌写进单元、输出或提交记录；需要授权时使用 Colab Secrets 等运行时机制。
- JPG 使用有损压缩。`subsampling=0` 表示 4:4:4、没有色度降采样，**不代表无损图像编码**；转为 RGB 后也不会保留 alpha 透明通道。

## English announcement

This Google Colab notebook, assembled by **PinKoalaXu**, brings together **Qwen-Image-2.1** and community models, a VAE, a multimodal text encoder, and five LoRA adapters in one deployment and editing workflow. It reduces manual setup by collecting dependency installation, model loading, adapter controls, inference, and downloads in a single notebook. The contribution here is workflow integration; all upstream models and components remain the work of their respective authors.

The default transformer is the ChatR Labs Uncensored Omni Step 90000 BF16 merged model, with official base-model and Turbo options. Optional Texture-Fix VAE and Heretic text encoder loading, five adjustable LoRA adapters, text-to-image generation, image editing with up to ten reference images, a Gradio interface, and high-quality JPG export are included. A separate Colab-native single-image upload/download workflow is also available.

The code includes LoRA key/fused-layer conversion, nonempty negative-prompt handling for True CFG, GPU residency/CPU offload selection, VAE tiling choices, and JPG export settings. These are implementation choices, not a guarantee that every bug is fixed or that every GPU, component combination, or output will work as expected.

**Licensing matters: Qwen-Image-2.1 and Turbo currently use the Qwen Research License. It permits non-commercial research or evaluation only; commercial use requires a separate license from the upstream rights holder.** Publicly downloadable weights do not imply unrestricted commercial permission. Each community component must also be reviewed individually.

**Community contributions are welcome:** fork the repository, make changes, and open a pull request for code, fixes, runtime reports, documentation, or translations. Suggestions are welcome in Issues / Discussions. The maintainer reviews and merges changes. Read [CONTRIBUTING.md](CONTRIBUTING.md), clear outputs and personal data, and preserve all upstream terms and attribution.

### Getting started

1. Select **Open in Colab**, choose a GPU runtime, and review the cells.
2. Run **1 → 2 → 3 → 3B** for GPU inspection, dependencies, base components, and LoRAs.
3. Use **4A** for a direct reference-image upload and JPG download, or **4B** for the Gradio interface.
4. Adjust components and resolution for available VRAM, host RAM, and storage. Full BF16 loading is resource intensive; free Colab runtimes are not guaranteed to work. Google controls runtime availability, quotas, disconnections, and charges.

This is a consolidated Colab entry point; first use still requires a GPU allocation, model downloads, and sequential cell execution. Turbo/community-adapter combinations require separate validation.

### Validation and privacy

- The notebook JSON and the Python syntax of all six code cells were checked, with Colab shell commands handled separately. GPU inference was not tested end to end. Dependencies and model revisions are not pinned, so upstream changes may break compatibility.
- Static inspection of the publication file found no personal email addresses, personal filesystem paths, common access tokens/API keys, IP addresses, saved outputs, or embedded attachments. This finding applies to this file, not to future runtime data.
- **Cell 4B defaults to `demo.launch(share=True, debug=True)`, creating a public temporary Gradio URL without authentication. Anyone holding that URL may be able to access the interface, submit jobs, and view data exposed by it. Do not upload confidential material or distribute the URL publicly; stop the runtime afterward.** Review debug output and logs before sharing.
- Execution contacts Google Colab, Hugging Face, GitHub, Python package services, and Gradio sharing services. Their terms and privacy policies apply. Keep credentials out of cells, outputs, and commits; use runtime secret storage when authorization is required.
- JPG is lossy. `subsampling=0` means 4:4:4 without chroma subsampling, **not lossless image compression**. RGB conversion also discards alpha transparency.

<a id="components-and-licensing"></a>
## 组件与授权 / Components and licensing

以下为笔记本引用的组件及公开页面的授权信息。功能描述为预期用途，不是独立性能验证。授权记录核对日期：**2026-11-12**；请始终检查实际下载版本的许可证、模型卡和附加要求。

The following entries reflect the notebook references and the licensing information on their public pages, reviewed on **2026-11-12**. Descriptions state intended roles, not independently verified performance. Always inspect the license, model card, and additional requirements for the exact revision you download.

| 类别 / Type | 来源与作者 / Source and author | 用途 / Intended role | 公开授权状态 / Published licensing |
| --- | --- | --- | --- |
| 基座 / Base | [Qwen-Image-2.1](https://huggingface.co/Qwen/Qwen-Image-2.1), [Turbo](https://huggingface.co/Qwen/Qwen-Image-2.1-Turbo) — Qwen | 图像生成与编辑 / Image generation and editing | Qwen Research License; non-commercial research/evaluation only |
| 1. 合并 Transformer / Merged transformer | [Uncensored Omni Quantized](https://huggingface.co/chatrlabs/Qwen-Image-2.1-Uncensored-Omni-Quantized) — ChatR Labs | Step 90000 BF16 合并版本；使用 `qwen-image-2.1-step90000-BF16` 子目录 / BF16 merged build from that subfolder | Qwen Research License |
| 2. VAE | [Texture-Fix VAE](https://huggingface.co/madebyollin/texture-fix-vae-for-qwen-image-2.1) — madebyollin | 纹理解码与伪影处理 / Texture decoding and artifact reduction | Qwen Research License |
| 3. 文本编码器 / Text encoder | [Text-Encoder-Heretic](https://huggingface.co/pottokao/Qwen-Image-2.1-Text-Encoder-Heretic) — pottokao | 基于 Qwen3-VL-8B-Instruct 的社区修改，保留视觉能力 / Community-modified Qwen3-VL-8B-Instruct encoder with vision support | Apache-2.0, according to its model card and LICENSE; does not change the image base model's terms |
| 4. LoRA | [Uncensored Omni LoRA v0.1](https://huggingface.co/chatrlabs/Qwen-Image-2.1-Uncensored-Omni-LoRA-v0.1) — ChatR Labs | 生成与编辑适配 / Generation and editing adapter | Qwen Research License |
| 5. LoRA | [Fix v2.0](https://huggingface.co/e-n-v-y/Qwen-Image-2.1-Fix-v2.0) — e-n-v-y | 细节与画面修复 / Detail and image refinement | Model card has no explicit license field; no root LICENSE was found during review. Additional permissions are unconfirmed. / 未确认附加授权 |
| 6. LoRA | [Detail Enhancer](https://huggingface.co/reverentelusarca/elusarcas-qwen-2.1-detail-enhancer-lora) — reverentelusarca | 细节增强与图像修复；触发词 `enhance this image` / Detail enhancement and restoration | No explicit license metadata or root LICENSE was found during review. Additional permissions are unconfirmed. / 未确认附加授权 |
| 7. LoRA | [Outfit-Swap & Consistency](https://huggingface.co/ausboss/Qwen-Image-2.1-Outfit-Swap-Consistency-LoRA) — ausboss | 换装时的一致性辅助 / Consistency during outfit editing | Model card declares Qwen Research License |
| 8. LoRA | [Natural Exposure](https://huggingface.co/prithivMLmods/Qwen-Image-2.1-Natural-Exposure-LoRA) — prithivMLmods | 自然、均衡曝光调整；实验预览 / Experimental neutral-exposure adjustment | Model card declares Qwen Research License and links to [PE-I2I LICENSE](https://huggingface.co/Qwen/Qwen-Image-2.1-PE-I2I/blob/main/LICENSE) |

“8 个社区组件”指 1 个合并 Transformer、1 个 VAE、1 个文本编码器及 5 个 LoRA，不含官方基座。ChatR Labs 的 BF16 Transformer 是 LoRA 合并版本，不应表述为已独立确认的全参数微调模型。

“Eight community components” counts one merged transformer, one VAE, one text encoder, and five LoRAs, excluding the official base. The ChatR Labs BF16 transformer is an adapter-merged model; this repository does not claim independent verification of full-parameter fine-tuning.

对于授权未明确的组件：公开可下载不代表放弃版权或授予无限制使用、再分发、改编及商用权利；基座许可证也不自动授予适配器作者的权利。取得明确授权前，请勿将其视为已获许可；可跳过 3B/相关加载代码，或自行移除对应 registry 项并确认所有加载分支均已停用。

For components with unclear permissions, public availability is not a waiver of copyright or an unrestricted license to use, redistribute, modify, or commercialize the component. The base license does not automatically grant the adapter author's rights. Obtain clarification before treating those uses as authorized; skip the relevant loading cell/code or remove the registry entries and ensure all loading paths are disabled.

<a id="legal-and-copyright"></a>
## 法律与版权声明 / Legal and copyright

### 中文

1. **独立社区项目与署名。** 本项目不隶属于、未经 Qwen、通义实验室、Alibaba、Google、Hugging Face 或任何组件作者背书。名称仅用于说明兼容对象与来源，不授予商标权。基座、权重、LoRA、VAE、编码器、代码与文档的版权和其他权利由各权利人保留。感谢全部上游作者及开源社区。
2. **遵守全部上游协议。** 本仓库发布的是笔记本及说明，不随仓库分发模型权重；运行时从上游下载。用户必须分别阅读并遵守实际使用版本的模型协议、许可证、NOTICE、署名、使用范围、修改标识与再分发要求。Qwen Research License 的非商业研究/评估限制与商业单独授权要求仍然适用，Apache-2.0 编码器或本仓库的说明均不能扩大基座授权。研究协议对衍生作品命名、适用的 “Built with Qwen” / “Improved using Qwen” 标识也有要求。
3. **协议副本与再分发。** 官方基座协议原文见 [上游 LICENSE](https://huggingface.co/Qwen/Qwen-Image-2.1/blob/main/LICENSE)；本仓库保留一份未修改的参考副本于 [licenses/Qwen-Image-2.1-LICENSE.txt](licenses/Qwen-Image-2.1-LICENSE.txt)，版权署名见 [NOTICE](NOTICE)。这不是对全部组件统一重新授权。若重新分发权重、修改后的上游材料或衍生模型，须核对并满足各自完整协议，包括适用的协议副本、NOTICE、修改说明及署名；本 README 不能替代它们。
4. **合法与经授权使用。** 不得用于违法内容、儿童性剥削材料、未经同意的私密影像或深度伪造、诈骗、冒充、骚扰，或侵犯版权、商标、隐私及肖像/人格权益的活动。仅上传有权使用且已取得必要同意的参考图片。遵守所在地法律、适用出口管制及 Colab、Gradio、GitHub、Hugging Face 等平台条款。“Uncensored”“Heretic”等名称不构成法律或协议义务的豁免。
5. **生成内容权利。** 本项目不保证生成内容具有版权、独占性、事实准确性或不侵权；技术上的生成能力不代表获得第三方作品、真实人物或品牌的许可。用户须自行审查输入、输出及其发布、传播和使用方式；适用法律或平台要求标注合成内容时，应进行标注。
6. **按现状提供与责任边界。** 在适用法律允许的范围内，本项目按现状提供，不作适销性、特定用途适用性、不侵权、安全性、可用性或运行结果保证。用户应评估算力费用、数据泄露、依赖变化、失败及生成结果风险。任何责任限制均以法律允许为限，不排除法律规定不可免除的责任，也不以本声明取代上游协议或专业法律意见。
7. **仓库原创内容。** 本次发布未为原创笔记本整合代码或文档额外指定 MIT、Apache-2.0 等许可证；公开仓库本身不等于授予额外版权许可。计划复用、改编或再分发原创内容时，请向维护者确认授权，并同时满足第三方条款。涉及权属或许可疑问，可通过本仓库 Issues 提出，勿公开私人资料或凭据。

### English

1. **Independent project and attribution.** This is an unofficial community integration, unaffiliated with and not endorsed by Qwen, Tongyi Laboratory, Alibaba, Google, Hugging Face, or component authors. Names identify compatibility and sources; no trademark rights are granted. All rights in upstream models, weights, adapters, VAEs, encoders, code, and documentation remain with their respective rights holders. We thank the upstream authors and open-source community.
2. **All upstream terms apply.** This repository distributes the notebook and documentation, not model weights; execution downloads weights from upstream sources. Users must separately comply with the exact versions' agreements, licenses, NOTICE files, attribution, scope-of-use, modification-notice, and redistribution requirements. Qwen Research License restrictions to non-commercial research/evaluation and separate commercial authorization remain applicable. Neither the encoder's Apache-2.0 license nor this README expands the image base model's permissions. The research agreement also includes naming requirements and applicable “Built with Qwen” / “Improved using Qwen” notices.
3. **License copies and redistribution.** Read the [official base LICENSE](https://huggingface.co/Qwen/Qwen-Image-2.1/blob/main/LICENSE). An unmodified reference copy is included at [licenses/Qwen-Image-2.1-LICENSE.txt](licenses/Qwen-Image-2.1-LICENSE.txt), with attribution in [NOTICE](NOTICE). This is not a blanket relicensing of all components. Redistributing weights, modified upstream materials, or derivative models requires compliance with each complete applicable agreement, including license copies, NOTICE files, change notices, and attribution. This README does not replace them.
4. **Lawful, authorized use.** Do not use this project for unlawful material, child sexual abuse material, non-consensual intimate imagery or deepfakes, fraud, impersonation, harassment, or infringement of copyright, trademarks, privacy, or personality/publicity rights. Use reference images only with sufficient rights and necessary consent. Comply with applicable law, export controls, and platform terms, including Colab, Gradio, GitHub, and Hugging Face. Names such as “Uncensored” and “Heretic” do not waive legal or contractual obligations.
5. **Output rights.** This project does not guarantee that outputs are copyrightable, exclusive, accurate, or non-infringing. Technical generation capabilities do not license third-party works, real people's likenesses, or brands. Users must review inputs, outputs, publication, distribution, and use, and disclose synthetic content where required by law or platform policy.
6. **As-is provision and liability.** To the extent permitted by applicable law, the project is provided as is without warranties of merchantability, fitness for a particular purpose, non-infringement, security, availability, or results. Users must assess compute costs, data exposure, changing dependencies, failures, and generated-content risks. Limitations apply only where legally permitted and do not exclude non-excludable liability. This statement does not replace upstream agreements or professional legal advice.
7. **Original repository content.** This publication does not add an MIT, Apache-2.0, or other license for the original notebook integration code or documentation. A public repository alone does not grant additional copyright permissions. Confirm permission with the maintainer for reuse, modification, or redistribution of original content, while also satisfying third-party terms. Raise rights or licensing questions through repository Issues without posting private data or credentials.
