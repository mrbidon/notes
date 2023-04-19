# Comptabilité partie double avec Dolibarr (France)

 ## Introduction
Système de comptabilité fiable inventé par les Vénitiens. Il s'agit que toutes les opérations fassent l'objet d'un débit dans un ou plusieurs comptes et d'un crédit dans un ou plusieurs autres comptes. De manière à ce qu'à tout moment la somme des débits est égale à la somme des crédits, on appelle cela la balance comptable. Cela permet plus de contrôle et permet d'enregistrer des dettes et des opérations futures, ce qui est impossible dans une comptabilité simple. [https://fr.wikipedia.org/wiki/Comptabilit%C3%A9_en_partie_double](source Wikipédia)


## Notion :
- **Compte** : il peut être crédité ou débité. Leur numérotation est normalisée par les services fiscaux [https://fr.wikipedia.org/wiki/Plan_comptable_g%C3%A9n%C3%A9ral_(France)](cf.Wikipédia plan comptable général (PCG))
- **Tier** : il s'agit d'un client, d'un fournisseur ou d'un employé, on peut associer un compte par tier. Dans le PCG, les comptes associés commenceront par les valeurs suivantes :
   - 40 fournisseur
   - 41 client
   - 42 Personnel.
- **Journal Général** :   Il constitue un document comptable obligatoire pour la grande majorité des structures. Il permet d’enregistrer chronologiquement toutes les opérations comptables de l’entreprise [https://www.appvizer.fr/magazine/finance-comptabilite/comptabilite/journal-comptable](source).
- **Lettrage**: Le lettrage comptable consiste à affecter au moins deux écritures comptables un code unique (composé de lettre de l'alphabet). La somme des entrées au crédit doit être égale à la somme des entrées au débit. Cette méthode permet de faire le lien entre une facture et son règlement. Il met en évidence les factures réglées (lettrées avec le(s) règlement(s)), des factures non réglées (non lettrées). Seuls les comptes de tiers peuvent être lettrés. [https://www.l-expert-comptable.com/a/6250-lettrage-comptable-definition-comment-le-faire.html](source)
- **Compte auxiliaire*: ils permettent d'assurer un meilleur suivi comptable des factures et paiements pour chaque tiers. [https://www.compta-facile.com/utilisation-comptes-auxiliaires-clients-fournisseurs/](source)


## Comptabilité dans Dolibarr

### Introduction
Le module évolue tranquillement depuis sa création environ en 2010, il permet de transformer "facilement" les opérations de caisse en opération comptable, il y a même des fonctions de clôture de compte, et surtout un moyen d'exporter vers beaucoup de logiciels de comptabilité propriétaire. Mais, il manque de la documentation. Nous avons arpenté le forum de ce logiciel pour livrer ici notre compréhension de la chose.

### Configuration
Avant toute chose, il est nécessaire de configurer le logiciel
- Comptabilité -> Configuration -> Plan Comptable  : il faut choisir le plan comptable que l'on souhaite utiliser pour la saisie comptable de notre organisation
- Comptabilité -> Configuration -> Compte par défaut : on configure les comptes par défaut associé à une vente de produit / de service, les comptes à débiter dans ce cas



### Configuration avancée
- Je veux que les clients aient un code propre comptable personnalisé commençant par 411
  - Aller dans le menu Accueil -> Configuration -> Modules / Application
  - Cliquez sur l'icône en forme d'engrenage, choisir selon le type de code personnalisé voulu :
    - Aquarium : 411 + code client ou 401 + code fournisseur
    - Digitaria : 411 + nom client ou 401 + nom fournisseur

### Saisir des opérations comptables
La première chose à comprendre, c'est que l'enregistrement d'une opération comptable est indépendante du reste du logiciel.

#### Saisir une opération comptable
    Aller dans le menu compta et
    
### Editer des opérations dans des journaux :
- Si il n'y en a pas beaucoup : supprimer et ajouter à la main l'opération qui correspond
- Si il y en a beaucoup :
  - exporter, éditer avec libreoffice par exemple
  - réimporter

### Annexe :
- [https://demo.noalyss.eu](Noalyz) Logiciel concurrent de comptabilité open source.
- Source / Discussion intéressante sur [https://www.dolibarr.fr/forum](le forum Dolibarr).
- [https://www.dolibarr.fr/forum/t/module-compta-pour-dolibarr/6727/118](Post de création du module compta)
- [https://wiki.dolibarr.org/index.php?title=Module_Comptabilit%C3%A9_en_Partie_Double](Doc officielle du module)
- [https://www.youtube.com/@accope/videos](Tuto intéressant pour néophyte sur la chaine YouTube accope)

