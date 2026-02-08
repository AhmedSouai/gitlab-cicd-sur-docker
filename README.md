# Pipeline CI/CD pour Mini-Projet GitLab sur l'environnement Docker

## 🎯 Objectif

Cette pipeline GitLab CI/CD automatise le **build, test, release et déploiement** de l'application Docker sur différents environnements (`REC`, `PREPROD`, `PROD`).  
Elle garantit que chaque commit est testé et que les déploiements sont fiables et reproductibles.

---

## ⚙️ Stages de la pipeline

1. **Build**
   - Construction d'une image Docker pour l'application.
   - L'image est taggée avec le **commit Git** pour versionner chaque build.
   - L'image est sauvegardée en artifact (`.tar`) pour être utilisée dans les tests et le release.

2. **Test**
   - Chargement de l'image Docker construite.
   - Lancement du conteneur et vérification qu'il répond correctement (via `curl` sur le port 80).
   - Permet de détecter rapidement les erreurs avant le push vers Docker Hub.

3. **Release**
   - Push de l'image Docker sur **Docker Hub** avec un tag unique correspondant au commit.
   - Garantit que chaque version déployée est identifiable et traçable.

4. **Deploy**
   - Déploiement automatique de l'image sur différents serveurs selon l'environnement :
     - `REC` (recette)
     - `PREPROD` (préproduction)
     - `PROD` (production) avec déclenchement **manuel** pour sécurité.
   - Les conteneurs sont remplacés proprement et configurés pour redémarrer automatiquement.

---

## 💡 Avantages de cette pipeline

- **Automatisation complète** : plus besoin d’interventions manuelles pour build/test/release.
- **Versioning précis** : chaque commit correspond à une image Docker unique.
- **Sécurité des déploiements** : PROD nécessite une validation manuelle.
- **Reproductibilité** : les environnements REC et PREPROD permettent de tester avant PROD.
- **Traçabilité** : grâce aux tags et artifacts, on sait quelle version a été déployée.

---

## 🔧 Bonnes pratiques

- Utiliser des **variables GitLab CI/CD** pour stocker les credentials (Docker Hub, SSH).
- Convertir les clés `.ppk` en format **OpenSSH** pour SSH.
- Ajouter des **healthchecks** pour s'assurer que le conteneur démarre correctement.
- Surveiller les logs lors des déploiements pour détecter rapidement les erreurs.
- Utiliser des tags `latest` si on souhaite redeployer facilement la dernière version.

---

## ⚡ Conclusion

Cette pipeline CI/CD rend le processus de développement et de déploiement **rapide, sûr et reproductible**, tout en offrant la possibilité de tester chaque version avant de la mettre en production.  
Elle est adaptée pour des environnements Docker et peut être adaptée pour des VMs classiques si nécessaire.

## Capture d'écran 
<img width="2293" height="782" alt="Capture d’écran 2026-02-08 154619" src="https://github.com/user-attachments/assets/33defeb6-dd63-48ed-a05f-52f10ab650e9" />

<img width="2558" height="1350" alt="Capture d’écran 2026-02-08 154750" src="https://github.com/user-attachments/assets/f4b30e59-921e-4aa8-af07-4ba2a862d67d" />

