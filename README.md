# Défi EGC 2024: Jeu de données Bitcoin

Pour toute question, contacter Remy Cazabet, remy.cazabet @ gmail com

## Sommaire
- [Challenges proposés](#exemples-de-challenges-auquel-répondre-dans-le-cadre-du-défi)
- [Séries temporelles](#séries-temporelles)
- [Réseaux de transactions](#Réseaux-de-transactions)
- [Questions fréquentes](#questions-fréquentes)

# Comment participer au défi EGC
Répondre au défi EGC consiste a soumettre à EGC 2024 un article synthétisant un travail de recherche portant ou utilisant les données fournies dans le cadre du défi. Cet article sera évalué (peer-review) par des membres du PC d'EGC, puis un vainqueur du défi sera choisi en fonction de ces évaluations. Le défi peut donc consister à répondre a différentes questions sur ce jeu de données, comme présenté ci-dessous. Les articles candidats au défi seront tous présentés dans un session réservée d'EGC.

# Challenges auquel répondre dans le cadre du défi
Toute contribution appliqué au jeu du données du défi peut être soumise comme participation au défi. Nous proposons plus particulièrement 2 challenges, plus un challenge libre.

* Séries temporelles : Prédiction de l'évolution du cours du Bitcoin. Ce défi consiste a prédire le cours du Bitcoin, en se basant non seulement sur le cours précédent, mais aussi sur les nombreuses autre séries temporelles fournies (acteurs, nombre de transactions, etc.), ainsi qu'éventuellement sur les séries de graphes.
* Graphes : Prédiction de liens, Prédiction de graphes. Disposant de multiples graphes correspondant à des journées différentes, mais impliquant les mêmes acteurs, il est possible de s'intéresser a prédire comment les intéractions entre ces acteurs vont évoluer au cours du temps, et donc de chercher a prédire les liens d'un graphe prochain, c'est à dire qui intéragira avec qui dans le futur, éventuellement avec les montants échangés. La tâche peut consister a prédire l'intégralité d'un graphe, ou a prédire certains liens cachés d'un graphe futur, a partir d'un apprentissage sur les graphes passés, voire en s'aidant des séries temporelles décrivant l'évolution de l'activité globale ou de certains acteurs particuliers.
* Objectif libre: De nombreuses autres contribution peuvent être proposées sur ces données, telles que des tâches de classification, de détection d'anomalies, de détection d'événements, de désanonysmisation (acteurs semblant différent mais ayant un comportement identique), etc.


### Description générale des données
Deux types de données sont fournis, synthétisant l'activité sur une période de 2 ans et demie, du 01/01/2015 au 30/06/2017:
* Des séries temporelles, décrivant l'activité générale de la Blockchain, ainsi que l'activité de 100 acteurs majeurs
* Des réseaux de transactions (1 par jour) décrivant les échanges entre un sous-ensemble d'acteurs majeurs

Les fichiers se trouvent dans ce dépôt Git.

# Séries temporelles
Toutes les séries temporelles ont une fréquence quotidienne (1 point=1 jour).
Les données sont fournies sous forme de csv, une colonne correspondant à la date, et les autres correspondant aux différentes séries temporelles

### Fichier external.csv
Ce fichier contient 2 séries temporelles, concernant des données qui ne sont pas issues de la blockchain Bitcoin, mais qui concernent l'économie Bitcoin: 
* `PriceUSD`: la valeur moyenne observée d'un Bitcoin en US dollar sur la journée sur les principales plateformes d'échange
* `HashRate`: Le HashRate (Taux de hachage), une mesure de la puissance de calcul totale utilisée par les miners https://en.bitcoinwiki.org/wiki/Hashrate

![Prix](https://github.com/Yquetzal/DefiEGC2024/blob/main/pics/ts_price.png?raw=true)

### Fichier blockchain_global.csv
Ce fichier contient des données aggrégées, calculées à partir des données de la blockchain Bitcoin. Les montants sont indiqués en Satoshis (https://en.bitcoin.it/wiki/Satoshi_(unit))
* `nb_transactions` : Nombre de transaction 
* `nb_payments`: Une transaction peut correspondre à plusieurs paiements, nombre total de paiements https://en.bitcoin.it/wiki/Transaction
* `total_received_satoshi` : Somme des valeurs reçues
* `total_sent_satoshi` : Somme des valeurs envoyées
* `total_fee` : Somme des montants payés en frais de transaction https://en.bitcoin.it/wiki/Miner_fees
* `mean_fee_satoshi` : Moyenne des frais payés par transaction
* `mean_feeUSD` : Moyenne des frais payés, en USD
* `mean_fee_for100` : Moyenne des montants des transactions payés en frais
* `mean_nb_inputs` : Nombre moyen de sorties par transaction https://en.bitcoin.it/wiki/Transaction
* `mean_nb_outputs` : Nombre moyen d'entrées par transaction https://en.bitcoin.it/wiki/Transaction
* `nb_mining` : Nombre de minages https://en.bitcoinwiki.org/wiki/Bitcoin_mining 
* `total_mining_satoshi` : Total des sommes perçues par les mineurs (BTC nouvellement créés et frais de transaction)
* `newly_created_coins` : Nombre de coins nouvellement créés et reçus par les mineurs
* `self_spent_satoshi`: Total des sommes que les acteurs se renvoient à eux-même (change, voir FAQ)

![global](https://github.com/Yquetzal/DefiEGC2024/blob/main/pics/ts_global.png?raw=true)


### Fichier blockchain_by_actor.csv
Ce fichier contient des séries temporelles décrivant les 100 acteurs ayant la plus grande activité (définie en nombre de jours d'activité) sur la période.
* `identity` : Identifiant de l'acteur, pouvant être un nom ou un numéro unique
* `received` : Total des montants reçu
* `spent` : Total des montants versé
* `nb_received` : Nombre de sorties de transactions reçues par l'acteur
* `nb_transactions` : Nombres de transactions faites par l'acteur
* `nb_spent` : Nombre de paiements faits par l'acteur (1 transaction = 1 ou plusieurs paiements).
* `sum_fee` : Total des frais de transactions payés par l'acteur pour les transactions dont il est la source
* `mean_fee_for100` : Moyenne des frais payés par transaction 
* `self_spent` : Montants observés comme envoyés de l'acteur à lui-même
* `self_spent_estimated` : Montants estimés comme probable envoie de l'acteur à lui-même, mais vers des adresses que nous ne connaissons pas. Cette valuer est forcément supérieure à `self_spent`.

![global](https://github.com/Yquetzal/DefiEGC2024/blob/main/pics/ts_actors.png?raw=true)


# Réseaux de transactions
Nous fournissons un réseau par jour sur la même période que les séries temporelles, à savoir du 01/01/2015 au 30/06/2017.

Le nom de chaque fichier indique le jour qu'il représente, au format YYYY-MM-DD

Les fichiers sont fournis au format csv, et représentent des graphes dirigés et pondérés, sous la forme de liste de liens. Chaque ligne correspond à un lien, et représente un résumé des échanges entre 2 acteurs pendant la journée. Pour choisir les acteurs, nous avons sélectionné les 10000 acteurs ayant le plus de jours d'activités sur la période d'étude. Seule une fraction d'entre eux sont présent chaque jour.
Le fichier est composé des colonnes suivantes : 
* `Source` : L'acteur à l'origine des échanges
* `Target` : L'acteur qui reçois les échanges
* `value` : Somme des montants envoyés par l'acteur Source à l'acteur Target pendant cette journée
* `nb_transactions` : Le nombre de transactions faites par Source à destination de Target pendant cette journée.

![Exemple de visualisation d'un réseau quotidien](https://github.com/Yquetzal/DefiEGC2024/blob/main/pics/network.png?raw=true)



# Questions fréquentes
### D'où proviennent les données ?
Les données ont été collectées dans le cadre du projet ANR BITUNAM http://cazabetremy.fr/BITUNAM.html . Les données de la blockchain Bitcoin sont publiques, et elles ont été enrichies avec une autre source publique, le site WalletExplorer https://www.walletexplorer.com , afin d'identifier le nom probable de certains acteurs

### Est-ce que les données sont fiables ?
Certaines données ne nécessitent pas de traitement et sont donc fiables, il s'agit du nombre de transactions, des montants échangés dans ces transactions, et du cours du Bitcoin. 

La plupart des autres données nécessitent de faire des pré-traitements, et en particulier d'identifier les "portefeuilles", ou ensembles d'adresses, appartenant à un même acteur. Cette procédure à été réalisée avec l'approche standard de clustering des adresses apparaissant en entrée des transactions, couramment utilisée dans la littérature (voir par exemple: "Harrigan, M., & Fretter, C. (2016, July). The unreasonable effectiveness of address clustering." https://arxiv.org/pdf/1605.06369.pdf). 

Cette méthode est connue pour avoir une bonne _Précision_ (Les adresses d'un cluster appartiennent effectivement au même acteur, sauf dans quelques cas évoqués ci-dessous, les CoinJoin), mais un _Rappel_ imparfait : nous ne découvrons qu'un sous-ensemble des adresses d'un utilisateur. Il est donc certain que les activités des acteurs sont des approximations conservatrices. Il s'agit cependant de la méthode la plus fiable existante, et les grandes quantités d'activité identifiées pour de nombreux acteurs connus montrent que les résultats sont suffisamment fiables pour pouvoir être interprétés.  Un problème connu qui conduit à ne pas avoir une Précision de 100% est qu'il est possible pour les acteurs de tromper les méthodes de clustering en utilisant des techniques que nous regroupons sous le nom de CoinJoin. Bien que les cas soient rares pour les acteurs importants, il y en a quelques-un d'identifiés dans ce jeu de données, en particulier l'acteur appelé ePay.info_CoinJoinMess, qui rassemblent les activités d'un Exchange connu (ePay), et d'un cluster d'adresses regroupées par des CoinJoins.

### A quoi correspondent les fee (frais de transactions) ?
Pour qu'une transaction Bitcoin soit effective, elle doit être inscrite dans la blockchaine. Cette tâche est accomplie par les mineurs, qui, en échangent, collectent 1) Des Bitcoins nouvellement créés et générés automatiquement pour chaque "bloc" créé, 2) Des frais de transactions dont le montant est fixé librement par le jeu de l'offre et de la demande (les mineurs ont intérêt à intégrer en priorité les transactions offrant les frais les plus élevés) (https://en.bitcoin.it/wiki/Miner_fees)

### A quoi correspondent les self-transactions (transactions de change) ?
Le protocole de Bitcoin utilise le principe de l'UTXO (https://en.wikipedia.org/wiki/Unspent_transaction_output), qui a pour conséquence que l'argent reçu par un acteur lors d'une transaction ne peut pas être dépensé partiellement, mais doit l'être dans sa totalité. L'usage courant est donc de payer le montant demandé et de s'envoyer le reste (le change) sur une _adresse de change_. Bien que celà apparaisse donc comme une transaction au sens de Bitcoin, il s'agit en fait d'une transaction d'un acteur vers lui-même. Les montants de ces transactions de change peut être énorme (si l'acteur A possede 1000 BTC et doit payer 1 BTC, il se renvoie 999 à lui-même). Les transactions de change sont détectés automatiquement en fonction des clusters d'adresses calculés, et sont donc à prendre comme des estimations conservatrices.

### A quoi correspondent les transactions des exchanges (gestionnaires de Wallet/plateformes d'échanges) ?
Les _Exchanges_, telles que Binance, Kraken ou Paymium, sont des entreprises proposant des services équivalents à ceux d'une banque dans le système monétaire classique. Elles permettent à des clients d'ouvrir des comptes chez eux, de transférer de l'argent sur ces comptes de et vers leur compte banquaire classique, ainsi que d'envoyer et de recevoir des transactions en Bitcoin, ou d'autres crypto-monnaies. Elles assurent également la conversion entre monnaies fiduciaires (Dollar, Euros...) et crypto-monnaies. Il est cependant important de comprendre qu'un compte ouvert chez une plateforme exchange ne correspond pas à l'ouverture d'un porte-monnaie sur la Blockchain : les comptes clients et leurs opérations ne sont jamais inscrit dans la Blockchain, et sont de simples écritures bancaires dans leurs bases de données internes. Les seules transactions observables dans la blockchain sont celles où un client demande à recevoir ou a envoyer des Bitcoins via une adresse Bitcoin. Une adresse Bitcoin est alors créée à la volée et la transaction demandée est inscrire dans la Blockchain. Du point de vue de la Blockchain, tous les comptes clients d'un exchange sont donc en fait un seul compte appartenant à l'exchange lui-même. Le transactions des exchanges sont donc (en majorité) des transactions de leurs clients.

### Est-ce que les transactions observées correspondent majoritairement à du trading ?
A priori, non. Bitcoin est effectivement une valeur spéculative, mais les opérations de trading (échanges Bitcoin<->Monnaie nationales) sont en fait des échanges entre clients des plateformes d'échanges, et ne sont pas inscrites dans la blockchain. Les activités de trading n'ont donc qu'un effet indirect sur les transactions de la blockchain présentent dans ce jeu de données (Exemple: Lorsque Bitcoin est dans une phase ascendante, il est probable que les clients investissent dans leurs comptes des Exchanges, et donc que les exchanges cherchent à acquérir de "vrai" Bitcoins sur la Blockchain)

### Est-ce que vous pourriez aussi partager les données de ... ?
Nous avons choisi de ne partager qu'un sous-ensemble des données à une granularité donnée pour ne pas rendre l'analyse trop complexe. Si vous êtes intéressé par d'autres données de la Blockchain, vous pouvez contacter les concepteurs du jeu de données (remy.cazabet@univ-lyon1.fr)

### Il me semble qu'il y a un problème/une erreur/quelque chose d'étrange
C'est tout à fait possible, n'hésitez pas à le signaler de préférence dans l'onglet "Issue" de ce dépôt afin que l'information soit visible par tous. Nous ferons de notre mieux pour corriger le problème.

