# Playbook pb-enrichissement-abuseipdb

| Paramètre | Valeur |
|---|---|
| Service | Azure Logic Apps (plan Consumption) |
| Modèle | Playbook with incident trigger |
| Déclencheur | Microsoft Sentinel incident |
| Connexion à Sentinel | Identité managée affectée par le système |
| Rôle de l'identité | Microsoft Sentinel Responder, sur le groupe de ressources |
| Région | Canada Central |

## Étapes
1. **Microsoft Sentinel incident** (déclencheur).
2. **Entités – Obtenir les IP** : liste d'entités = `Entities` du déclencheur.
3. **For each** sur les IP :
   1. **HTTP**
      - Méthode : `GET`
      - URI : `https://api.abuseipdb.com/api/v2/check`
      - En-têtes : `Key: <clé d'API AbuseIPDB>`, `Accept: application/json`
      - Requêtes : `ipAddress = IP Adresse`, `maxAgeInDays = 90`
      - Paramètres : **Secure inputs activé**
   2. **Parse JSON** : contenu = `Body` de HTTP, schéma = [`schema-abuseipdb.json`](schema-abuseipdb.json)
   3. **Ajouter un commentaire à l'incident (V3)** : ID ARM de l'incident + message = [`message-commentaire.txt`](message-commentaire.txt)
