---
title: "Processus d'Engagement POC dans SAP (POC Commitment Process in SAP)"
type: "knowledge_base"
status: "Proposition digitale — POC exploratoire, non validé comme processus cible"
approach: "Évaluer d'abord le standard SAP pour mesurer les possibilités de l'ERP et le fit/gap"
tags: [sap, wholesale, commitment_process, mto, supply_chain]
last_updated: "2026-09-29"
source: "https://docs.google.com/document/d/1rJG7Xr7CO3Zey7gsqzKspMcDCREy0_xs9s_6F8QuF3Q/edit?tab=t.0#heading=h.eey97vn00j56"
summary: "Proposition digitale pour évaluer en standard SAP un processus d'engagement Wholesale fondé notamment sur les contrats et Scheduling Agreements. Le POC vise à mesurer le fit/gap avant toute décision sur la cible."
---

# Processus d'Engagement POC dans SAP (POC Commitment Process in SAP)

> **Positionnement** : cette proposition du Digital est une démarche exploratoire, pas un processus cible validé. Le premier temps consiste à tester le concept en standard SAP pour comprendre les possibilités de l'ERP et mesurer le fit/gap. Les processus, périmètres, jalons et responsabilités détaillés ci-dessous sont donc à valider.

## 1. Contexte et Objectifs du POC

### Contexte General
Le projet s'inscrit dans une réflexion globale sur la modélisation des flux Wholesale dans l'ERP SAP Decathlon, en s'inspirant des meilleures pratiques du secteur [1].

### Objectifs Metier
* **Gestion de la Demande (Demand)** :
  * Faire cohabiter un approvisionnement basé sur les prévisions (*forecasts*) avec un modèle d'engagement (*commitment*) [1].
  * Intégrer les besoins Wholesale directement au sein des signaux de demande globale [1].
  * Basculer d'un mode de fonctionnement *Make to Stock* (MTS) vers un mode *Make to Order* (MTO) pour les commandes sous engagement [2].
* **Expédition et Distribution (Dispatch)** :
  * Transformer le processus d'approvisionnement réactif et manuel en un processus proactif et automatisé [1].
  * Anticiper la descente de stock et la réservation par partenaire à partir des données amont (engagements ou commandes fermes) [1].
  * Exploiter le signal du `Delivery Plan` pour optimiser le taux de service et maximiser l'OTIF (*On-Time In-Full*) [3].

### Indicateurs Clés de Performance (KPIs)
* **Amélioration du taux de service** sur les commandes partenaires [2].
* **Amélioration de l'OTIF** [2].
* **Satisfaction utilisateur** (Key Account Managers - KAM, Sales Admin, client final) [2].
* **Suivi de la DSI**, écoulement du stock (comparatif *commitment-forecast* vs *ventes-écoulement*) et ratio marge/stock [2].

---

## 2. Hypothèse de processus à évaluer et principes proposés

### Principes Directeurs
1. **Obligation du Delivery Plan** : Tout processus de *Commitment* exige la saisie systématique d'un `Delivery Plan` [3].
2. **Saisie des données** : Le contrat et le `Delivery Plan` doivent être renseignés dès la phase de sélection ou immédiatement après [3].
3. **Responsabilité de saisie** : Le `Delivery Plan` est saisi par le KAM, poussé par le ZMP ou défini selon un calendrier établi par Decathlon [4].

### Flux Documentaire SAP (Core Process Inbound & Outbound)

1. **Contrat (`Contract VAL/QTY`)** : Création d'un contrat cadre pour la saison avec des lignes d'articles (`1 item line`) [3].
2. **Programme d'échéancier (`Scheduling Agreement` - SA)** : Génération des lignes d'échéances (`Schedule Lines`, type de document `ZLN`, `SP: CAR`) ajustées selon les besoins partenaires [3].
3. **Demande d'Achat (`Purchase Request` - PR)** : Création automatique des DA multi-lignes [3]. Les DA générées sont identifiées en MTO et ignorées par le calcul du MRP classique [6].
4. **Commande d'Achat (`Purchase Order` - PO)** : Génération automatique des POs (`type de document ZBWS`) [3].
5. **Réception / Entrée de Marchandise (`MIGO`)** : Réception en CAC (`GR / CAC`) [3].
6. **Réservation du Stock** : Le stock arrivant en zone est réorienté et strictement réservé pour honorer le contrat souscrit [7].
7. **Commande de Vente Partner (`Sales Order`)** : Orchestration via l'OMS SAP B2B. Génération de la livraison (`OBD`) uniquement sur présence de stock physique, suivie de la sortie de marchandise (`PGI / CAR`) [2, 3].

---

## 3. Périmètre et Critères de Validation du Pilote (POC)

### Périmètre Applicatif
* **Canal de distribution** : Resell (les réseaux de Franchise sont exclus du périmètre V0 du POC) [9].
* **Planning de démarrage** : Lancement du POC prévu pour octobre 2026 [9].

### Critères de Sélection des Partenaires
* **Adresse de livraison** : Obligation d'avoir une adresse de livraison unique (*single ship-to*) [9, 12].
* **Typologie d'articles** : Capacité à gérer des articles mono et multi-variantes [12, 13].
* **Sourcing** : Un seul fournisseur en MTO [12].
* **Couverture géographique** :
  * 1 partenaire situé en Zone [9, 12].
  * 1 partenaire situé en Europe (partenaire retenu : `Bergfreunde`) [9, 12, 13].
* **Ressources humaines** : Mobilisation d'un Sales Admin expérimenté et d'un ZMP désigné pour piloter le POC [9, 12].
* **Profil de commande** : Existence de réassorts réguliers au cours de la saison (*repeat*) [9, 13].
* **Contraintes logistiques V0** : Pas de conditionnement ni de services additionnels spécifiques requis [10, 12].
* **Capacité partenaire** : Fourniture anticipée d'un `Delivery Plan` exploitable [13].

### Points à Valider Durant le Pilote
* **Transversalité (Cross)** :
  * Validation du lien de bout en bout entre contrat, `Delivery Plan`, PO/PR et commandes de vente [4].
  * Arbitrage entre approvisionnement dédié par partenaire et exigences de massification de la production [4].
  * Évaluation du catalogue de services Supply Chain et définition de l'arbre de décision pour la validation des contrats [5].
* **Demande (Demand)** :
  * Comportement des PR/PO générés sur la base des commitments [6].
  * Analyse des impacts liés au contournement du MRP classique [6].
* **Expédition (Dispatch)** :
  * Compatibilité des objets SAP (`Contract`, `Scheduling Agreement`) avec les données métiers amont [7].
  * Rétention et réservation stricte du stock dédié lors de son arrivée en zone [7].
  * Vérification de la non-régression sur les autres canaux de distribution (CORE Decathlon et New Business Models) [7].

---

## 4. Contraintes Techniques, Limites et Points Ouverts

### Contraintes Techniques Identifiées
* **Transfert Inter-Sites (CAC > CAR)** :
  * La différence de valorisation des stocks entre les différents `Plants` (zones d'évaluation distinctes) empêche le transfert direct CAC > CAR sous sa forme standard [3].
  * *Pistes de résolution* : Étude des fonctionnalités de Cross-Docking (`Xdock`) ou utilisation de clés d'approvisionnement spéciales (*Special Procurement Key*) [3].

### Synthèse des Points Ouverts
| Catégorie | Point Ouvert / Problématique | Piste ou Action Associée |
| :--- | :--- | :--- |
| **Logistique & Stock** | Entrepôt source pour les commandes Resell (préparation en CAC vs descente en CAR) [8, 13]. | Arbitrage selon règles de conditionnement [8]. |
| **Gestion WMS** | Visibilité du stock dédié Commitment au niveau WMS et rapport MRP [8, 10]. | Étude d'une zone de stockage dédiée (`Storage Location`) [10, 11]. |
| **SI & Interfaces** | Définition de la stratégie Front-End pour la saisie du contrat [8]. | SAP/Vibecoding à court terme, Dealer Portal à long terme [8]. |
| **Gouvernance** | Flexibilité contractuelle (gestion des variations de volume en % et modifications in-season) [8]. | Ajustement possible des `Delivery Plans` ou `Sales Orders` [8]. |
| **Facturation** | Calcul des coûts de cession et valorisation des stocks [8, 16]. | Harmonisation des règles de facturation [8]. |

---

## 5. Feuille de Route et Prochaines Étapes

### Calendrier de Déploiement (Roadmap 2026-2027)

```
2026
├── Juillet - Août : Tests Contrats & SA en Préproduction / Validation config SAP [9]
├── Septembre     : Création Contrat & SA pour SS27 (1 Reseller / Bergfreunde) [9]
├── Octobre       : Paramétrage SAP par l'expert technique [9, 15]
├── 3 Novembre    : Validation en Comité Fonctionnel [14]
└── Q4 (Nov-Déc)  : Exécution des PO/PR et ajustement de l'allocation downstream [9]

2027
├── Q1            : Soft Freeze & finalisation des ajustements inter-équipes [15]
└── Q2            : Suivi de la réception, réservation du stock et mesure de l'OTIF [9]
```

### Gouvernance et Responsables d'Actions
* **Coordination Générale Projet** : Olivier Verscheure & Émilie L. [11]
* **Alignement Périmètres Digitaux** : Loïc Dubart, Paul Peruzetto, Cédric Montay, Camille Wattier, Lucie Baudin [11]
* **Modèle Opérationnel Business (Operating Model)** : Olivier Verscheure [11]
* **Paramétrage Technique SAP** : Jean-Marc Dickes (mission démarrant début octobre 2026) [3, 11]
* **Isolation Stock / Storage Location** : Camille Wattier & Pierre Blanpain [11]
* **Cadrage Opérationnel Bergfreunde** : Cédric Montay [11]
* **Validation Métier & Logistique** : Fred Gentes, Emeline Ducrest, Magali Bonnin, Esther, Fred D., Arif, Shikriti [11, 14]
