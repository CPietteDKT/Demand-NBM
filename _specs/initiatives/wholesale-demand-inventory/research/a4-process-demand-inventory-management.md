---
title: "A4 - PROCESS - DEMAND & INVENTORY MANAGEMENT / WHOLESALES - 2026"
type: "knowledge_base"
status: "Document de travail métier — état As-Is et propositions To-Be"
tags: [supply_chain, wholesale, resell, demand_management, inventory_management, sap]
last_updated: "2026-09-29"
source: "https://docs.google.com/document/d/1627Un3dpCxy5-xbyF9aSa-J9og5wrw5USZBLksFbtoE/edit?tab=t.0"
summary: "Document de travail métier sur les processus Demand & Inventory Management pour Wholesale / Resell, notamment les saisies multi-horizons et l'approche de flag des PO Wholesale en saison. Il décrit les flux As-Is et les propositions To-Be."
---

# A4 - Process Demand & Inventory Management (Wholesales - Resell)

> **Statut** : document de travail métier. Les éléments décrits comme To-Be et les questions ouvertes ne constituent pas, à eux seuls, des décisions validées.

## 1. Contexte & Alignement Général

### Objectifs & Périmètre
* **Finalité** : Intégration globale de la demande et de la gestion des stocks pour le nouveau modèle économique **Wholesale - Resell** (partenaires sous engagement / *Commit*).
* **Portée Géographique** : Monde entier, structuré par Zone d'Approvisionnement (`Supply Zone`).
* **Horizons Temporels** : Multi-horizon (Stratégique, Tactique, Pré-Saison, En-Saison).
* **Parties Prenantes Majeures** :
  * **Intervenants amont** : `ZMP` (Zone Supply Manager), `ZMPM`, `Key Account Manager` (KAM), Équipes Wholesale locales.
  * **Destinataires des flux** : `PSP`, `PSS`, `ZDP`, `RDP`.
  * **Gouvernance & Process Owners** : Nicolas PHAM (Demand & Inventory Planning), Mathilde BUCHTA (Economic Framework), Clara DEMON (RESELL), Sofia M. (Project Manager NBM).

### Exclusion du Périmètre A4 actuel
* **B2B Traditionnel** : Non inclus dans le flux A4 actuel (arbitrage futur si intégration requise).
* **External Marketplaces** (ex: *T-Mall*) : Non incluses (absence d'outils calibrés pour fournir des prévisions multi-horizons à cette granularité).

### Cartographie des Zones d'Approvisionnement (`SZ` / `CZ`)
Les besoins Wholesale doivent être saisis par zone géographique dédiée :
* **`SZ EUROPE`** : PO DPMI, PO UK, PO Switzerland.
* **`SZ MEA`** : PO Morocco, PO Tunisia, PO Egypt, PO Booster Marseille, PO Israël, PO Turkey.
* **`SZ NEA`** : PO China, PO HK.
* **`SZ SEA`** : PO Thailand, PO Vietnam, PO Indonesia, PO Australia, PO Algeria, PO Booster Malaysia, PO Taiwan, PO Japan, PO South Korea.
* **`SZ LATAM`** : PO Booster America, PO Mexico, PO Colombia, PO Chile.
* **`CZ CANADA`** : PO Canada, PO USA.
* **`CZ INDIA`** : PO India.
* **`CZ BRAZIL`** : PO Brazil.

### Familles & Gammes Prioritaires (Volumétrie)
Priorité d'implémentation accordée aux gammes à fort enjeu économique :

| Famille Produit | Marque / Tag | Codes Familles SAP / FIORI |
| :--- | :--- | :--- |
| **`#BIKES`** | **VAN RYSEL** | `01 259`, `10 218`, `35 132`, `35 303` |
| **`#FOOTWEAR`** | **KIPRUN** | `11 886`, `11 887`, `01 500`, `21 500` |
| **`#METALS`** | **DOMYOS** | `12 072`, `34 970`, `00 699`, `00 702` |

---

## 2. Processus "As Is" par Horizon Temporel

### 1. Horizon Tactique (2026 - 2028)
* **Système & Saisie** : Création d'une colonne dédiée `Wholesales` dans l'interface **`FIORI`** (Vue *Plan Super Models* / `SWO`).
* **Niveau de Granularité** : Saisie des volumes au niveau **Code Conception (`CC`)** par zone (`SZ`/`CZ`).
* **Processus d'Engagement** :
  * Les équipes Wholesale locales fournissent les quantités `CC` au `ZMP` dès fiabilisation des données.
  * Date limite de saisie dans les colonnes Wholesale par le `ZMP` : **Semaine 24 WW (W.24 WW)**.
  * Les trajectoires globales par Sport / `UI` sont validées au niveau central.

### 2. Horizon Pré-Saison

#### A. Saisie des Prévisions de Commande (RFQ & Sélection)
* **Prévisions de Ventes (*Sales Forecast*)** : Pas de saisie de ventes en Pré-Saison (*No Gesture, No Sales*).
* **Prévisions d'Achats (*Purchase Forecast*)** : Saisie manuelle des volumes d'achat Wholesale via un fichier centralisé Google Sheet transmis aux `ZMP`.
* **Renseignements des colonnes** :
  * Étape **RFQ** : Renseignement de la colonne `SWO` dans le module *Country Selection RFQ*.
  * Étape **Initial Selection** : Renseignement de la colonne `SWO` dans *Country Selection SSV*.
* **Engagement Ferme (*COMMIT*)** : Toute quantité renseignée en Pré-Saison constitue un **engagement ferme (`COMMIT`)** pour l'organisation Wholesale.

#### B. Gestion des Grilles de Tailles (*Gridsize*)
* **Catalogue Spécifique Wholesale (`SMU WHOLESALES`)** : Gestion de la grille de tailles sur mesure selon les demandes du partenaire Wholesale.
* **Catalogue Traditionnel Decathlon** : **Aucune modification de la grille de tailles** globale pour éviter de déstabiliser le besoin Decathlon Core. La grille de tailles doit être ajustée uniquement au niveau du Bon de Commande / Ordre de Fabrication (`Work Order` / `WO`).

#### C. Impact Économique & Synthèse
* **Principe d'Isolation** : Dans le processus As-Is, les quantités saisies sous la colonne `SWO` sont **exclues de la Synthèse Économique** (aucun impact direct sur les indicateurs *T.O*, *Cession T.O*, *Supply Margin*, *KS Margin*).

### 3. Horizon En-Saison

#### A. Conversion des Engagements en Demandes d'Achat
* Passage de l'engagement Pré-Saison (`SWO Purchase Commit`) vers l'émission de la Demande d'Achat (`PR`) et du Bon de Commande (`WO`) grâce à l'application d'un plan de livraison dans le système.
* **Schéma Directeur de Livraison** :
  * **Option 1 (Directe / *Highway*)** : Plan de livraison formellement communiqué par l'équipe Wholesale locale et appliqué directement dans le système.
  * **Option 2 (Exception)** : Absence de plan de livraison transmis ; le `ZMP` applique une préconisation standard préfinie.

#### B. Passation & Flag des Commandes dans SAP
* Création manuelle de la Demande d'Achat / Commande d'Achat via la transaction SAP **`ZME21N`** avec marquage explicite du **Flag `Wholesales`**.
* **Utilisation actuelle du Flag** :
  * Séparation/Fusion des besoins (*Split/Merge*).
  * Identification des lignes réservées `PSS`.
  * Extraction manuelle pour le suivi de la dévalorisation des stocks.

#### Complément métier communiqué le 29 septembre 2026

* Dans l'approche en saison décrite comme As-Is, les commandes d'achat Wholesale sont marquées d'un flag et exclues du calcul du besoin. Cette exclusion ne fonctionne toutefois pas de bout en bout, car la synchronisation avec l'aval n'a pas été réalisée.
* En anticipation, les quantités Wholesale Resell sont saisies dans `PQZD` et `SSV`.
* **À réconcilier** : le document présente aussi l'exclusion du calcul MRP comme une évolution To-Be ; la qualification As-Is ci-dessus décrit une approche déjà tentée mais inopérante faute de synchronisation aval.

---

## 3. Processus Cible "To Be" & Améliorations Système

```
[ Pré-Saison : SWO Commit ] ──> [ Contrat SAP (ex: SPEEDO) ] ──> [ Neutralisation du besoin dans le Calcul MRP Core ]
                                                                        │
                                                                        ▼
                                                       [ Réservation Automatique du Stock ]
```

### Évolutions Fonctionnelles Requis

1. **Modélisation par Contrat SAP (Type `SPEEDO`)**
   * Création d'un contrat cadre SAP par partenaire/revendeur (*Reseller*).
   * Chaque commande ferme d'un revendeur est automatiquement déduite du contrat associé.

2. **Neutralisation dans le calcul du Calcul de Besoin (`MRP`)**
   * Exclure les commandes et demandes d'achat Wholesale du calcul du besoin Decathlon Core pour éviter le sur-approvisionnement ou le manque de stock réseau.
   * Conservation de la visibilité des lignes Wholesale dans le rapport `MRP Report` à titre informatif.

3. **Automatisation des Réservations de Stock**
   * **In-Season As-Is (Manuel)** : La réservation de stock nécessite une intervention manuelle du KAM une fois le produit dans le réseau, créant un décalage d'indexation lors des calculs `CBN` du lundi.
   * **In-Season To-Be (Automatique)** : La présence du Flag `Wholesales` déclenche une réservation automatique du stock physique et exclut la quantité du besoin global disponible.

4. **Mesure de la Performance & Indicateurs (`KSI`)**
   * Définition d'un cadre d'exclusion ou d'intégration spécifique pour mesurer la fiabilité des prévisions d'achat Wholesale (`KSI Purchase Forecast Reliability`).
   * Structuration de la gouvernance en cas d'écart par rapport au contrat de service (`GTCS` - *Global Terms and Conditions of Sale*, ex: tolérance de 10% en Europe).

---

## 4. Matrice des Questions Ouvertes & Responsabilités

| Sujet / Point Ouvert | Enjeu Fonctionnel | Pilote / Responsable |
| :--- | :--- | :--- |
| **Format d'Input Wholesale** | Définir le canal et le niveau de granularité standard pour les saisies (Qty `CC` vs Qty Modèle + Grille de tailles). | Nicolas DESPLANQUES, Clara DEMON, Isabel MARTINS |
| **Contrat de Service & GTCS** | Formalisation du cadre contractuel (ex: seuil de tolérance 10% Europe, pénalités en cas de Gap volume). | Nicolas DESPLANQUES, Clara DEMON |
| **Impact Synthèse Économique** | Intégration ou maintien du masquage des flux Wholesale dans les arbitrages financiers. | Mathilde BUCHTA |
| **Mesure KSI Forecast Reliability** | Isoler l'impact des variations Wholesale sur la note de fiabilité des prévisions d'achat. | Nicolas PHAM, Théophile MORIN, Digital Team |
| **Granularité par Reseller** | Obtenir un suivi individuel par partenaire/revendeur au sein du volume global modèle. | Nicolas PHAM, Théophile MORIN, Digital Team |
| **Mécanisme de Dé-réservation** | Définir les règles de gouvernance pour libérer du stock réservé non consommé et le réinjecter dans le besoin Core. | Nicolas PHAM |
