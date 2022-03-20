# Défi EGC Bitcoin
Cette page décrit le défi pour EGC 2023 - Lyon : Analyse des données Bitcoin

## Description des données
Deux types de données sont fournies:
* Séries temporelles
* Réseaux de transactions

# Séries temporelles
Toutes les séries temporelles concernent une période de 2 ans et demie, du 01/01/2015 au 30/06/2017, et ont une fréquence quotidienne (1 point=1 jour).
Les données sont fournies sous forme de csv, une colonne correspondant à la date, et les autres correspondant aux différentes séries temporelles

### Fichier external.csv
Ce fichier contient 2 séries temporelles, concernant des données qui ne sont pas issues de la blockchain Bitcoin, mais qui concernent l'économie Bitcoin: 
* `PriceUSD`: la valeur moyenne observée d'un Bitcoin en US dollar sur la journée sur les principales plateformes d'échange
* `HashRate`: Le HashRate (Taux de hachage), une mesure de la puissance de calcul totale utilisée par les miners https://en.bitcoinwiki.org/wiki/Hashrate

### Fichier blockchain_global.csv
Ce fichier contient des données aggrégées, calculées à partir des données de la blockchain Bitcoin. Les montants sont indiqués en Satoshis (https://en.bitcoin.it/wiki/Satoshi_(unit))
* `nb_tr` : Nombre de transaction 
* `value` : Somme des valeurs des sorties des transactions
* `sum_fee` : Somme des montants payés en frais de transaction https://en.bitcoin.it/wiki/Miner_fees
* `mean_nb_inputs` : Nombre moyen de sorties par transaction https://en.bitcoin.it/wiki/Transaction
* `mean_nb_outputs` : Nombre moyen d'entrées par transaction https://en.bitcoin.it/wiki/Transaction
* `nb_mining` : Nombre de minages https://en.bitcoinwiki.org/wiki/Bitcoin_mining 
* `sum_mining` : Total des sommes perçues par les mineurs (BTC nouvellement créés et frais de transaction)

### Fichier blockchain_by_actor.csv
Ce fichier contient des séries temporelles décrivant les 100 acteurs ayant la plus grande activité (définie en nombre de jours d'activité) sur la période.
* `identity` : Identifiant de l'acteur, pouvant être un nom ou un numéro unique
* `received` : Total des montants reçu
* `nb_received` : Nombre de sorties de transactions reçues par l'acteur
* `sum_fee` : Total des frais de transactions payés par l'acteur pour les transactions dont il est la source
* `spent` : Total des montants versé
* `nb_spent` : Nombre de transactions dont cet acteur est la source.

# Réseaux de transactions
Nous fournissons un réseau par jour sur la même période que les séries temporelles, à savoir du 01/01/2015 au 30/06/2017.

Le nom de chaque fichier indique le jour qu'il représente.
Les fichiers sont fournis au format csv, et représentent des graphes dirigés et pondérés, sous la forme de liste de lien. Chaque ligne correspond à un lien, et représente un résumé des échanges entre 2 acteurs pendant la journée. Pour choisir les acteurs, nous avons sélectionné les 10000 acteurs ayant le plus de jours d'activités sur la période d'étude.
Le fichier est composé des colonnes suivantes : 
* `Source` : L'acteur à l'origine des échanges
* `Target` : L'acteur qui reçois les échanges
* `value` : Somme des montants envoyés par l'acteur Source à l'acteur Target pendant cette journée
* `nb_transactions` : Le nombre de transactions faite par Source à destination de Target pendant cette journée.
