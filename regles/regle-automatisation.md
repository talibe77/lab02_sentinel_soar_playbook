# Règle d'automatisation

| Paramètre | Valeur |
|---|---|
| Nom | Enrichissement AbuseIPDB – Force brute par IP |
| Déclencheur | Quand un incident est créé |
| Condition | Nom de la règle analytique contient « Force brute RDP par IP » |
| Action | Exécuter le playbook pb-enrichissement-abuseipdb |
| Expiration | Indéfinie |
| Ordre | 1 |

La condition limite l'automatisation aux incidents qui contiennent des entités IP : les incidents de la règle « distribuée » n'en ont pas.
