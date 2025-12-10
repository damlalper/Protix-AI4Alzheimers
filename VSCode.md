# 🟢 AŞAMA 2 — VSCode (Backend + Frontend + Deployment)

## 1️⃣ Backend (FastAPI + GPU inference + Multi-modal API)

### 1.1 API Tasarımı

| Endpoint                   | Method | Input                                                                                  | Output                                                                                                       | Açıklama                                      |
|----------------------------|--------|----------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|-----------------------------------------------|
| /predict_binding           | POST   | JSON { "protein_sequence": "...", "ligand_smiles": "..." }                             | JSON { "binding_score": float, "predicted_residues": [...], "attention_map": [...], "3D_coords": [...] }  | Protein-ligand binding tahmini                |
| /visualize_3d              | POST   | JSON { "protein_id": "...", "ligand_id": "..." }                                        | 3D interactive plot link veya iframe embed                                                                 | PyMol/Three.js 3D visualization               |
| /protein_embedding         | GET    | protein_id                                                                             | embedding vector                                                                                             | Frontend veya downstream modeller için       |
| /ligand_embedding          | GET    | ligand_id                                                                              | embedding vector                                                                                             | Frontend veya downstream modeller için       |
| /multi_modal_analysis      | POST   | JSON { "protein_seq": "...", "ligand_smiles": "...", "clinical_data": {...} }          | JSON { "combined_score": float, "explanation": {...} }                                                      | Multimodal fusion modeli ile skor ve explainable AI |

### 1.2 Backend Yapısı

/backend
│
├─ main.py # FastAPI entrypoint
├─ models/
│ ├─ protein_model.pt # Colab-trained protein GNN/Transformer
│ ├─ ligand_model.pt # Colab-trained ligand GNN
│ ├─ multimodal_model.pt # Multimodal fusion (protein+ligand+clinical)
│
├─ utils/
│ ├─ preprocess.py # SMILES -> graph, fasta -> embedding
│ ├─ inference.py # model forward + explainability
│ ├─ visualization.py # 3D plots, attention maps
│
├─ requirements.txt
├─ Dockerfile
└─ README.md


- GPU-enabled inference (`torch.cuda.is_available()`)  
- Batch processing (multi-query API)  
- Logging: W&B / Prometheus  
- Validation: schema validation via Pydantic  

## 2️⃣ Frontend (React + 3D Visualization + Dashboards)

### 2.1 UI / UX Yapısı

**Dashboard:**

- Protein seçim (UniProt ID)  
- Ligand seçim (DrugBank/ChEMBL)  
- Optional: multimodal inputs (MRI metadata, clinical features)  

**Outputs:**

- Binding score & heatmaps  
- Attention / XAI visualization  
- 3D protein-ligand structure (Three.js)  
- Protein / ligand embeddings TSNE/UMAP plots  

**Interactivity:**

- Rotate/zoom 3D protein-ligand  
- Hover residues for predicted binding info  
- Toggle attention heatmaps  

### 2.2 Tech Stack

- React.js + TypeScript  
- Plotly.js / Dash / Three.js  
- Axios / WebSocket for API calls  
- Responsive UI (Bootstrap / TailwindCSS)  

### 2.3 Folder Structure

/frontend
│
├─ src/
│ ├─ components/
│ │ ├─ ProteinSelector.tsx
│ │ ├─ LigandSelector.tsx
│ │ ├─ BindingScoreCard.tsx
│ │ ├─ ThreeDViewer.tsx
│ │ ├─ AttentionHeatmap.tsx
│ │
│ ├─ pages/
│ │ ├─ Dashboard.tsx
│ │ └─ MultiModalAnalysis.tsx
│ │
│ ├─ utils/
│ │ └─ api.ts # Axios + WebSocket wrapper
│ │
│ └─ App.tsx
├─ public/
└─ package.json


## 3️⃣ Data Integration (Backend + Frontend)

**Backend inference pipeline → Frontend JSON API**  

**JSON Input:**
```json
{
  "protein_sequence": "MGSSHHHHHHSSGLVPRGSH...",
  "ligand_smiles": "CC(=O)OC1=CC=CC=C1C(=O)O",
  "clinical_features": {"age": 72, "MMSE": 28}
}
```
JSON Output:
```json

{
  "binding_score": 0.87,
  "predicted_residues": [12, 45, 102],
  "attention_map": [[...]],
  "3D_coords": {"protein": [...], "ligand": [...]},
  "explainability": {"residue_importance": [...], "ligand_contrib": [...]}
}
```

**Frontend bu JSON’u alıp:**

- 3D görselleştirir  
- Embedding ve attention heatmap çizer  
- Dashboard günceller  

## 4️⃣ Deployment (Docker + CI/CD)

### 4.1 Docker

- GPU destekli container  
- FastAPI + Uvicorn + Torch  
- Frontend container React build + Nginx  

### 4.2 CI/CD

- GitHub Actions:  
  - Test: unit + integration  
  - Build: Docker image  
  - Deploy: AWS ECS / GCP Cloud Run / Azure Container Instances  

### 4.3 Optional Real-time

- WebSocket ile 3D viewer update + model inference streaming  
- Async queue (Celery + Redis) for large batches  

## 5️⃣ Visualization / Reporting

- Protein-ligand 3D interaktif viewer  
- Attention / Grad-CAM overlay  
- TSNE / UMAP embedding plot (protein seq & ligand)  
- Multi-modal fusion dashboard (binding score + clinical features)  
- Export: PDF/HTML reports for each prediction  

## 6️⃣ Outputs for Portfolio / CV

| Output                         | Açıklama                                      |
|--------------------------------|-----------------------------------------------|
| Interactive 3D Viewer           | Frontend showcase, Three.js                   |
| Binding Prediction API           | Backend + JSON API                             |
| Multi-modal Fusion Dashboard     | Protein + ligand + optional clinical features |
| Explainable AI Visualization    | Attention / SHAP / Grad-CAM overlays          |
| Dockerized Deployment            | CV’de “production-ready AI system” olarak gösterilebilir |
| CI/CD Pipeline                   | GitHub Actions + automated test/build/deploy  |

✅ Bu yapı, Colab’da eğittiğimiz modeli sorunsuz bir şekilde VSCode tarafına entegre ediyor, frontend-backend interaktif sistem haline getiriyor ve portfolio / CV için maksimum teknik değer katıyor.

## 7️⃣ VSCode – Ek Gereklilikler ve İyileştirmeler (Test, API, Security, vs.)

### 1️⃣ Testler (Unit, Integration, E2E)

**Unit Test (pytest)**

- Veri ön işleme fonksiyonları (`preprocess.py`)  
- Ligand graph embedding ve protein embedding fonksiyonları  
- FastAPI endpoint logic testleri (mock input/output)  

**Integration Test**

- API endpointler → model inference → output JSON  
- Multi-modal fusion pipeline testi  
- 3D viewer / frontend API call testleri (mock backend)  

**End-to-End Test (E2E)**

- Kullanıcı protein ve ligand seçimi → binding score ve 3D görselleştirme → explainable AI overlay  
- Selenium veya Playwright ile frontend + backend entegrasyonu  

**CV/Portfolio Katkısı:**  
“Test yazılım geliştirme pratiği, reliability ve reproducibility göstergesi.”

### 2️⃣ API Yönetimi ve Dokümantasyon

- FastAPI otomatik OpenAPI dokümantasyonu  
- Swagger UI veya Redoc entegrasyonu  
- Rate limiting & throttling (örn. 100 request / dakika)  
- CORS ve authentication:  
  - Token-based auth (JWT)  
  - Sağlık projelerinde veri erişimi kontrolü  

**CV/Portfolio Katkısı:**  
“Professional API design & documentation, secure health data handling”

### 3️⃣ Güvenlik ve Compliance

- HIPAA / GDPR gibi veri yönetimi standartlarına uygun mock data kullanımı  
- Input validation & sanitization (SMILES, protein sequences)  
- Logging & monitoring:  
  - Hangi API çağrıları yapıldı, hangi model kullanıldı  
  - Error tracking (Sentry veya Prometheus)  
- Docker container security:  
  - Image vulnerability scan (Trivy, Clair)  
  - GPU container isolation  

**CV/Portfolio Katkısı:**  
“Sağlık AI projelerinde veri gizliliği ve güvenlik bilinçli geliştirme”

### 4️⃣ Data Management & Versioning

- Model checkpoints version control (Git + DVC veya MLflow)  
- Input datasets versioning (UniProt, PDB, DrugBank)  
- Logging inference data + output (anonymized for HIPAA/GDPR)  

**CV/Portfolio Katkısı:**  
“Reproducible & auditable scientific AI pipeline”

### 5️⃣ Performance ve Scalability

- GPU inference optimization  
- TorchScript veya ONNX export  
- Batch inference endpoint  
- Async queue (Celery + Redis) for heavy multi-modal computations  

### 6️⃣ Monitoring / Dashboard / Logging

- Real-time logs ve metrics (Prometheus + Grafana)  
- API usage metrics (number of predictions, latency)  
- Model performance drift monitoring (tracking accuracy over time)  

### 7️⃣ Ek Özellikler / Sağlık Projelerinde Mantıklı Olanlar

- Explainable AI dashboard: SHAP / Grad-CAM görselleştirmeleri, residue importance  
- Multi-modal fusion: protein + ligand + klinik metadata + optional: MRI/omics features  
- 3D Protein-Ligand Viewer: interaktif, hover-over residue info, rotation/zoom  
- PDF / HTML Export: binding report, explainable AI visuals, embeddings plots  

**CV/Portfolio Katkısı:**  
“End-to-end health AI platform, interpretable, interactive, reproducible”

### Özet: VSCode’da Eklenmesi Mantıklı Katmanlar

| Kategori      | Önerilen Ekler                                      | CV / Portfolio Katkısı                        |
|---------------|----------------------------------------------------|-----------------------------------------------|
| Test          | Unit, Integration, E2E                              | Reliability, reproducibility                  |
| API           | Swagger/OpenAPI, JWT auth, rate limiting           | Professional API design                        |
| Security      | Input validation, logging, container scan          | Health-data compliance (HIPAA/GDPR)          |
| Data          | Versioning (DVC/MLflow), anonymization             | Reproducible pipelines                         |
| Performance   | TorchScript / ONNX, async queue                     | Scalable AI inference                          |
| Monitoring    | Prometheus/Grafana, usage metrics                   | Production-readiness                            |
| Visualization | 3D viewer, SHAP/Grad-CAM, dashboards               | Interactive & explainable AI                   |
