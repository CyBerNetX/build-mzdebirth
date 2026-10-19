# Build_MzDebirth

Chaîne de build Dockerisée pour [MzDebirth](https://github.com/simozzer/MzDebirth)
(collection de synthés Korg Mz-series).

## Principe

`docker-compose.yml` construit dans un conteneur **Ubuntu 22.04** (glibc 2.35)
pour produire un `.deb` compatible Ubuntu 22.04 / 24.04 / 26.04.

- Récupère automatiquement la dernière release via l'API GitHub
- Clone JUCE + les dépôts Mz* au premier lancement (dans `srcs/`)
- Emballe en `.deb` avec `assets/control` comme template (`@VERSION@`)
- Vérifie que le binaire ne requiert pas une glibc trop récente

## Utilisation

```bash
docker compose up          # build complet
ls out/                    # → mzdebirth_<version>_amd64.deb
tail -f out/build.log      # suivi du build

rm -rf srcs/* && docker compose up

## Fichiers

docker-compose.yml	        Pipeline de build
assets/control	            Template du paquet .deb (placeholder @VERSION@)
assets/mzdebirth.desktop	Lanceur d'application
out/	                    .deb produits + build-history.txt

