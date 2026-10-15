# NEXUS-NVIDIA
nexus_nvidia` regroupe les dépendances GPU nécessaires au fonctionnement de la plateforme **NEXUS** sous forme d'archives compressées, afin de permettre un déploiement hors-ligne (air-gapped) ou sur des machines sans accès aux dépôts NVIDIA / PyPI.
# NEXUS NVIDIA

> Bundle de composants de la pile GPU NVIDIA (CUDA / TensorRT / Triton) packagés
> en archives `.tar.lzma` et pilotés par une application Python unique.

![status](https://img.shields.io/badge/status-⟨alpha|beta|stable⟩-blue)
![python](https://img.shields.io/badge/python-⟨3.x⟩-yellow)
![license](https://img.shields.io/badge/license-⟨MIT|GPL--3.0|proprietary⟩-lightgrey)

---

## Présentation

`nexus_nvidia` regroupe les dépendances GPU nécessaires au fonctionnement de la
plateforme **NEXUS** sous forme d'archives compressées, afin de permettre un
déploiement hors-ligne (air-gapped) ou sur des machines sans accès aux dépôts
NVIDIA / PyPI.

Le point d'entrée applicatif est `nexus_app.py`.

---

## Contenu du dépôt

### Sources / bibliothèques décompressées

| Dossier | Rôle |
|---|---|
| `cudnn-frontend` | Frontend C++ pour cuDNN |
| `cutlass` | Templates CUDA pour opérations GEMM / tenseurs |
| `dali` | NVIDIA Data Loading Library (prétraitement) |
| `nccl` | NVIDIA Collective Communications Library (multi-GPU) |
| `nexus_hook_supreme` | ⟨hook interne NEXUS — décrire ici⟩ |
| `rapids-cudf` | RAPIDS cuDF (DataFrames GPU) |
| `tensorrt` | Moteur d'inférence TensorRT |
| `triton-inference-server` | Serveur d'inférence Triton |

### Archives distribuables

```
cudnn-frontend.tar.lzma
cutlass.tar.lzma
dali.tar.lzma
nccl.tar.lzma
rapids-cudf.tar.lzma
tensorrt.tar.lzma
triton-inference-server.tar.lzma
```

### Application

```
nexus_app.py        # point d'entrée principal
```

---

## Prérequis

- Linux x86_64 (⟨version testée⟩)
- Pilote NVIDIA ≥ ⟨version⟩
- CUDA Toolkit ⟨version⟩
- Python ⟨3.10+⟩
- Espace disque : prévoir ⟨taille totale⟩ (les archives font plusieurs Go ;
  le poste de référence affichait moins de 8 Go libres pendant l'extraction)

---

## Installation

1. Cloner le dépôt :

```bash
git clone https://github.com/⟨utilisateur⟩/nexus_nvidia.git
cd nexus_nvidia
```

2. Décompresser les archives nécessaires :

```bash
for f in *.tar.lzma; do tar --lzma -xf "$f"; done
```

3. Créer l'environnement Python et installer les dépendances :

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

4. Vérifier la disponibilité du GPU :

```bash
nvidia-smi
```

---

## Utilisation

```bash
python nexus_app.py ⟨options⟩
```

⟨Documenter ici les arguments CLI, les variables d'environnement et un exemple
de sortie attendue.⟩

---

## Arborescence

```
nexus_nvidia/
├── cudnn-frontend/
├── cutlass/
├── dali/
├── nccl/
├── nexus_hook_supreme/
├── rapids-cudf/
├── tensorrt/
├── triton-inference-server/
├── *.tar.lzma
└── nexus_app.py
```

---

## Notes de déploiement

- Les archives `.tar.lzma` sont destinées à être copiées telles quelles vers un
  support externe (SSD / HDD) puis extraites sur la machine cible.
- Prévoir un support disposant d'au moins ⟨taille⟩ d'espace libre : la copie
  échoue silencieusement si la destination est pleine.
- ⟨Ajouter ici toute contrainte de version croisée entre TensorRT, CUDA et le
  pilote.⟩

---

## Feuille de route

- [ ] Ajouter un script `install.sh` idempotent
- [ ] Empreintes SHA-256 pour chaque archive
- [ ] CI de vérification d'intégrité
- [ ] ⟨…⟩

---

## Contribution

Les issues et pull requests sont bienvenues. Merci de suivre le template fourni
et de décrire précisément l'environnement (pilote, CUDA, version de Python).

---

## Licence

⟨Préciser la licence. Attention : les composants NVIDIA redistribués ici sont
soumis aux NVIDIA Software License Agreements respectifs — vérifier les droits
de redistribution avant publication publique.⟩
