Comptabilité partie double avec Dolibarr

Sytème de comptabilité fiable inventé par les véniciens. Il s'agit que toutes les opérations fassent l'objet d'un débit dans un ou plusieurs compte et d'un crédit dans un ou plusieurs autre compte. De manière à ce qu'à tout moment la somme des débits est égale à la somme des crédits, on appelle cela l balance comptable. Cela permet plus de contrôle et permet d'enregistrer des dettes et des opérations futures.

(source : https://fr.wikipedia.org/wiki/Comptabilit%C3%A9_en_partie_double)


Notion :
- compte : il peut être crédité ou débité. Ils sont normalisés par les services fiscaux (https://fr.wikipedia.org/wiki/Plan_comptable_g%C3%A9n%C3%A9ral_(France)) 
- tier : un client, un fournisseur ou un employé, on peut associé un compte par tier, il commencera selon le type de tier : 401 fournisseur, 411 client ou 421 Rénumération du personnel.
- journal : 
- Lettrage: Le lettrage comptable consiste à affecter à au moins deux écritures comptables un code unique (composé de lettre de l'alphabetr). La somme des entrées au crédit doit être égale à la somme des entrées au débit. Cette méthode permet de faire le lien entre une facture et son règlement. Il met en évidence les factures réglées (lettrées avec le(s) règlement(s)), des factures non réglées (non lettrées). Seuls les comptes de tiers peuvent être lettrés.

(source https://www.l-expert-comptable.com/a/6250-lettrage-comptable-definition-comment-le-faire.html)

- Compte auxiliaire : il permet d'assurer un meilleur suivi comptable des factures et paiements pour chaque tier . 
(source  https://www.compta-facile.com/utilisation-comptes-auxiliaires-clients-fournisseurs/)


Comptabilité dans dolibar :
Le module évolue tranquillement, mais il manque de la documentation. Nous avons appenté le forum pour pour vous livrer ici notre compréhension de la chose.

Configuration dans dolibar :
- Compte : On configure les comptes par défaut associé à une ventre de produit / de service, les compte à débiter dans ce cas


Configuration
- Je veux choisir le code 
- Je veux que les clients aient un code propre comptable qui commence par 411 
        * Aller dans le menu Acceuil -> Configuration -> Modules / Application 
        * Cliquez sur l'icone en forme d'engrenage choisir soit :
            Aquarium : 411 + code client ou 401 + code fournisseur
            Digitaria : 411 + nom client ou 401 + nom fournisseur

- choisir 


FAQ :
Saisir une opération comptable 
    Aller dans le menu compta et 
    
Editer des opérations dans des journaux :
    Supprimer et ajouter à la main l'opération qui correspond

    Si il y en a beaucoup :
    - exporter, éditer avec libreoffice par exemple
    - réimporter


concurent compta open source dolibarr 
https://demo.noalyss.eu


Source / Discussion intéressante sur le forum dolibarr

Création du module compta : https://www.dolibarr.fr/forum/t/module-compta-pour-dolibarr/6727/118

Doc officielle du module : https://wiki.dolibarr.org/index.php?title=Module_Comptabilit%C3%A9_en_Partie_Double



Tuto intéressant sur https://www.youtube.com/@accope/videos
