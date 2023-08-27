# Comptabilité en partie double avec Dolibarr (France)

 ## Introduction
La comptabilité en partie double (où compte de contrepartie) est un système fiable inventé par les Vénitiens. Il s'agit que toutes les opérations fassent l'objet d'un débit dans un ou plusieurs comptes et d'un crédit dans un ou plusieurs autres comptes associés. De manière à ce qu'à tout moment la somme des débits est égale à la somme des crédits, on appelle cela la balance comptable. Cela permet plus de contrôle et permet d'enregistrer des dettes et des opérations futures, ce qui est impossible dans une comptabilité simple. Source: [Wikipédia](https://fr.wikipedia.org/wiki/Comptabilit%C3%A9_en_partie_double), [site debitoor](https://debitoor.fr/termes-comptables/compte-de-contrepartie)


## Notion :
- **Compte** : il peut être crédité ou débité. Leur numérotation est normalisée par les services fiscaux [cf.Wikipédia plan comptable général (PCG)](https://fr.wikipedia.org/wiki/Plan_comptable_g%C3%A9n%C3%A9ral_(France))
- **Tier** : il s'agit d'un client, d'un fournisseur ou d'un employé, on peut associer un compte par tier. Dans le PCG, les comptes associés commenceront par les valeurs suivantes :
   - 40 fournisseur
   - 41 client
   - 42 Personnel.
- **Journal Général** :   Il constitue un document comptable obligatoire pour la grande majorité des structures. Il permet d’enregistrer chronologiquement toutes les opérations comptables de l’entreprise [source](https://www.appvizer.fr/magazine/finance-comptabilite/comptabilite/journal-comptable).
- **Lettrage**: Le lettrage comptable consiste à affecter au moins deux écritures comptables un code unique (composé de lettre de l'alphabet). La somme des entrées au crédit doit être égale à la somme des entrées au débit. Cette méthode permet de faire le lien entre une facture et son règlement. Il met en évidence les factures réglées (lettrées avec le(s) règlement(s)), des factures non réglées (non lettrées). Seuls les comptes de tiers peuvent être lettrés. [source](https://www.l-expert-comptable.com/a/6250-lettrage-comptable-definition-comment-le-faire.html)
- **Compte auxiliaire*: ils permettent d'assurer un meilleur suivi comptable des factures et paiements pour chaque tiers. [source](https://www.compta-facile.com/utilisation-comptes-auxiliaires-clients-fournisseurs/)


## Comptabilité dans Dolibarr

### Introduction
Le module évolue tranquillement depuis sa création environ en 2010, il permet de transformer "facilement" les opérations de caisse en opération comptable, il y a même des fonctions de clôture de compte, et surtout un moyen d'exporter vers beaucoup de logiciels de comptabilité propriétaire. Mais, il manque de la documentation. Nous avons arpenté le forum de ce logiciel pour livrer ici notre compréhension de la chose.

### Configuration
Avant toute chose, il est nécessaire de configurer le logiciel
- Comptabilité -> Configuration -> Plan Comptable  : il faut choisir le plan comptable que l'on souhaite utiliser pour la saisie comptable de notre organisation
- Comptabilité -> Configuration -> Compte par défaut : on configure les comptes par défaut associé à une vente de produit / de service, les comptes à débiter dans ce cas



### Configuration avancée
#### Je veux que les codes clients ou fournisseurs soient la même chose que les code comptables 411 ou 401

A la base ce comportement n'est pas possible, j'ai donc soumis un patch qui sera intégré aux prochaines versions dolibar. Si vous souhaitez faire fonctionner ce patch en avance de phase suivez les étapes suivantes :
  - sauvegarder votre base de donnée
  - Updater les codes existants via la requête vers des codes en 401 (à adapter)
```
   -- mise à jour du format code_client vers le format comptable 
   UPDATE llx_societe SET code_client = CONCAT('411', LPAD(SUBSTR(code_client, 8), 5,'0') )
   WHERE code_client IS NOT NULL AND code_fournisseur  IS NULL;  

   -- copie du code_client en code_comptable
   UPDATE llx_societe SET code_compta = code_client WHERE code_compta IS NULL;
         
   -- mise à jour du format code_fournisseur vers le format comptable
   UPDATE llx_societe SET code_fournisseur = CONCAT('401', LPAD(SUBSTR(code_fournisseur, 8), 5,'0') ) 
   WHERE code_client IS NULL AND code_fournisseur  IS NOT NULL;

   -- copie du code_fournisseur en code_compta_fournisseur 
   UPDATE llx_societe SET code_compta_fournisseur = code_fournisseur WHERE  code_compta_fournisseur IS NULL;   
   
   -- insertion du paramètre caché permettant d'activer la recopie du code client ou fournisseur sans préfix
    INSERT INTO llx_const (name, entity, value, type, visible, note, tms)
    VALUES('COMPANY_AQUARIUM_NO_PREFIX', 1, '1', 'chaine', 0, '', '2023-04-27 00:54:28.496');
```

  - ajouter les modifications à la main ou via cherry-pick en modifiant les fichiers selon la pull request suivante https://github.com/Dolibarr/dolibarr/pull/24705/files
    - `htdocs/core/modules/societe/mod_codecompta_aquarium.php` 
    - `htdocs/langs/en_US/admin.lang`       
  - activer "Elephant" avec la valeur "411{00000}" pour les clients "401{00000}" pour les fournisseurs
  - activer "Aquarium", vérifier que le message est bien affiché : "Do not use prefix, only copy cutomer or supplier code = yes" 
  - c'est bon maintenant les codes compta seront utilisé partout dans l'application

### Saisir des opérations comptables
La première chose à comprendre, c'est que l'enregistrement d'une opération comptable est indépendante du reste du logiciel.

#### Saisir une opération comptable à la main
Aller dans le menu compta et cliquer sur l'icone + et suivez les insctructions
    
#### Editer des opérations dans des journaux :
- Si il n'y en a pas beaucoup : supprimer et ajouter à la main l'opération qui correspond
- Si il y en a beaucoup :
  - exporter, éditer avec libreoffice par exemple
  - réimporter

### Annexe :
- [Noalyz](https://demo.noalyss.eu) Logiciel concurrent de comptabilité open source.
- Source / Discussion intéressante sur [le forum Dolibarr](https://www.dolibarr.fr/forum).
- [Post de création du module compta](https://www.dolibarr.fr/forum/t/module-compta-pour-dolibarr/6727/118)
- [Doc officielle du module](https://wiki.dolibarr.org/index.php?title=Module_Comptabilit%C3%A9_en_Partie_Double)
- [Tuto intéressant pour néophyte sur la chaine YouTube accope](https://www.youtube.com/@accope/videos)

