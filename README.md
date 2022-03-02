# Défi EGC Bitcoin
Cette page décrit le défi pour EGC 2023 - Lyon : Analyse des données Bitcoin

## Description des données
Deux types de données sont fournies:
* Séries temporelles
* Réseaux de transactions

### Séries temporelles
Toutes les séries temporelles concernent une période de 2 ans et demie, du 01/01/2015 au 30/06/2017, et ont une fréquence quotidienne (1 point=1 jour).

#### Fichier external.csv
Ce fichier contient 2 séries temporelles, concernant des données qui ne sont pas issues de la blockchain Bitcoin, mais qui concernent l'économie Bitcoin: 
* **PriceUSD**: la valeur moyenne observée d'un Bitcoin en US dollar sur la journée sur les principales plateformes d'échange
* **HashRate**: Le HashRate (Taux de hachage), une mesure de la puissance de calcul totale utilisée par les miners https://en.bitcoinwiki.org/wiki/Hashrate
