<!-- NeuroAssist AI · README by Usama Shahid (fewgets) -->
<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0D1117,55:0F3D3E,100:36FFC7&height=230&section=header&text=NeuroAssist%20AI&fontSize=60&fontColor=FFFFFF&fontAlignY=36&desc=Brain%20tumour%20detection%20and%20glioma%20stage%20prediction&descSize=17&descAlignY=58&animation=fadeIn" width="100%" alt="NeuroAssist AI"/>

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=22&duration=3000&pause=700&color=36FFC7&center=true&vCenter=true&width=720&height=60&lines=CNN+for+MRI+Tumour+Classification;ANN+for+Glioma+Stage+Prediction;Deep+Learning+for+Healthcare" alt="Typing SVG"/>

<p>
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python"/>
  <img src="https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white" alt="PyTorch"/>
  <img src="https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white" alt="FastAPI"/>
  <img src="https://img.shields.io/badge/OpenCV-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white" alt="OpenCV"/>
  <img src="https://img.shields.io/badge/Vercel-000000?style=for-the-badge&logo=vercel&logoColor=white" alt="Vercel"/>
  <img src="https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikitlearn&logoColor=white" alt="scikit-learn"/>
</p>

<p>
  <a href="https://neuroassistai.vercel.app/"><b>🌐 Live Demo</b></a> · <a href="https://www.kaggle.com/datasets/masoudnickparvar/brain-tumor-mri-dataset"><b>📁 Dataset</b></a> · <a href="https://onlinelibrary.wiley.com/doi/full/10.1155/2022/1830010"><b>📜 Research Paper</b></a>
</p>

</div>

---
## 📌 Overview

**NeuroAssist AI** is a two-stage deep-learning system that supports doctors in brain-tumour diagnosis:

1. 🧠 **Tumour Detection:** a custom **CNN** classifies an MRI scan as *Glioma*, *Meningioma*, *Pituitary* or *No Tumour*.
2. 🧬 **Glioma Staging:** if a glioma is found, a custom **ANN** predicts its **stage** from gene-mutation test results.
3. 💡 **Guidance:** each result comes with clear, plain-language precautions.

It is served through a **FastAPI** backend and a **live web app**, so anyone can try it in the browser.

> 🌐 **Try it now:** [neuroassistai.vercel.app](https://neuroassistai.vercel.app/)

---

## 🖼️ Sample MRI Classes

| Glioma | Meningioma | Pituitary | No Tumour |
|:-:|:-:|:-:|:-:|
| <img src="images/glioma.jpg" width="160"/> | <img src="images/mengioma.jpg" width="160"/> | <img src="images/pituitary.jpg" width="160"/> | <img src="images/notumor.jpg" width="160"/> |

---

## 🔬 Pipeline

```mermaid
flowchart LR
    MRI[🩻 MRI scan] --> CNN[🧠 CNN<br/>tumour classifier]
    CNN -->|Glioma| GENE[🧬 Gene-mutation<br/>test results]
    GENE --> ANN[🟢 ANN<br/>stage predictor]
    CNN -->|Meningioma / Pituitary / None| OUT[📋 Result]
    ANN --> OUT
    OUT --> GEM[💡 Precautions]
```

---

## 🧠 Model Architecture

### 🔷 CNN: Brain Tumour Classification

| Layer | Details |
|---|---|
| Input | Grayscale MRI image |
| Feature extractor | 3 × (Conv2D → ReLU → MaxPool) |
| Classifier | Flatten → Dense → Softmax |
| Output | 4 classes: Glioma, Meningioma, Pituitary, No Tumour |
| Accuracy | **≈ 93%** on the test set |

*Trained from scratch in PyTorch on an NVIDIA GPU.*

### 🟢 ANN: Glioma Stage Prediction

| Layer | Details |
|---|---|
| Input | 9 features: gender, age and mutation status of **IDH1, TP53, ATRX, PTEN, EGFR, CIC, PIK3CA** |
| Hidden | 2–3 fully connected layers with ReLU |
| Output | Glioma stage |

---

## 📚 Research Basis

Based on the paper **"Brain Tumor Classification and Glioma Stage Prediction Using Deep Learning"**
([Wiley, 2022](https://onlinelibrary.wiley.com/doi/full/10.1155/2022/1830010)).
The paper published no code, so the full pipeline was **implemented from scratch**.

**Dataset:** [Brain Tumor MRI Dataset (Kaggle)](https://www.kaggle.com/datasets/masoudnickparvar/brain-tumor-mri-dataset): 4 classes of grayscale MRI images.

---

## 🔌 API Endpoints

| Method | Endpoint | Purpose |
|---|---|---|
| `GET` | `/` | Health check |
| `POST` | `/predict-image` | Upload an MRI image and get the tumour class |
| `POST` | `/predict-glioma-stage` | Send gene-mutation values and get the glioma stage |

---

## 🚀 Run Locally

```bash
git clone https://github.com/fewgets/NeuroAssistAI.git
cd NeuroAssistAI
pip install torch torchvision opencv-python pillow numpy scikit-learn fastapi uvicorn python-multipart
```

**Model files**

| File | Model | Where |
|---|---|---|
| `glioma_stages.pth` | Glioma stage ANN | ✅ Included in `models/` |
| `BTD_model.pth` | Tumour CNN | 📥 [Download from Google Drive](https://drive.google.com/file/d/19SVLCD3DTa1aBZ9PI4TTgNkvJKgL2LSY/view?usp=drive_link) and place it in `models/` (too large for GitHub) |

```bash
uvicorn API:app --reload      # API at http://127.0.0.1:8000/docs
# or
python main.py
```


---

## 📁 Project Structure

```text
NeuroAssistAI/
├── API.py              # FastAPI endpoints
├── main.py             # Entry point
├── utils.py            # Input helpers and precautions
├── models/
│   ├── TumorModel.py   # CNN and ANN definitions
│   └── glioma_stages.pth
└── images/             # Sample MRI scans
```

---

## 🔭 Roadmap

- [ ] LLM-powered medical Q&A for patients
- [ ] Grad-CAM heatmaps to show *where* the model is looking
- [ ] Doctor dashboard with patient history
- [ ] Mobile app

> ⚠️ **Disclaimer:** for research and education only. It is not a medical device and must not be used for clinical decisions without professional validation.

---

## 🤝 Let's Work Together

<div align="center">

**Have an idea, a freelance project, or want to collaborate on something in AI?**
I'm always open to collaborations, freelance work and full-time opportunities.

<a href="mailto:shaikhusama541@gmail.com?subject=Collaboration%20-%20NeuroAssist%20AI">
  <img src="https://img.shields.io/badge/Email-shaikhusama541%40gmail.com-36FFC7?style=for-the-badge&logo=gmail&logoColor=white&labelColor=0D1117" alt="Email"/>
</a>
<a href="https://www.linkedin.com/in/-usamashahid/">
  <img src="https://img.shields.io/badge/LinkedIn-Usama%20Shahid-36FFC7?style=for-the-badge&logo=linkedin&logoColor=white&labelColor=0D1117" alt="LinkedIn"/>
</a>
<a href="https://github.com/fewgets">
  <img src="https://img.shields.io/badge/GitHub-fewgets-36FFC7?style=for-the-badge&logo=github&logoColor=white&labelColor=0D1117" alt="GitHub"/>
</a>

<br/><br/>

⭐ **If you like this project, please give it a star. It really helps!** ⭐

<br/>

<h3>"AI won't replace doctors, but it can give them a second pair of eyes."</h3>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:36FFC7,55:0F3D3E,100:0D1117&height=150&section=footer&animation=twinkling" width="100%" alt="footer"/>

</div>
