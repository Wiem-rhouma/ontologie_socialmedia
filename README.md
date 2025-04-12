# ontologie_socialmedia
Phase 1 : Choix du domaine Domaine sélectionné : 
Réseaux sociaux 

Justification du choix du domaine : 
Le domaine des réseaux sociaux est très pertinent pour la modélisation sémantique car il comprend de nombreux concepts interconnectés tels que les utilisateurs, les publications, les groupes, les commentaires, etc. Ce domaine est : • Facile à comprendre et très actuel. • Riche en relations et hiérarchies. • Idéal pour appliquer SPARQL, OWL et SWRL (ex. : suggestion d’amis, détection d’interactions). Il s'agit également d’un domaine très présent dans le web et bien documenté dans des vocabulaires sémantiques comme FOAF, ce qui permet une meilleure réutilisation des namespaces standards.

Phase 3 :  interrogation avec SPARQL :

requete 1: pour tester les instances des moderateurs et leur groupe :
PREFIX : <http://www.semanticweb.org/administrator/ontologies/2025/3/socialmedia#>
SELECT ?moderateur ?nom ?groupe WHERE { 
?moderateur a :Moderateur . 
?moderateur :nom ?nom . 
?moderateur :modère ?groupe . 
?groupe :nomGroupe ?nomGroupe . }

requete 2: Lister les membres qui publient des publications:
PREFIX : <http://www.semanticweb.org/administrator/ontologies/2025/3/socialmedia#>
SELECT ?auteur ?nom ?contenu WHERE {
  ?auteur a ?type .
  FILTER (?type = :Membre || ?type = :Modérateur) .
  ?auteur :nom ?nom .
  ?auteur :publie ?pub .
  ?pub :contenu ?contenu .
}

requete 3: Trouver les groupes sans modérateur :
PREFIX : <http://www.semanticweb.org/administrator/ontologies/2025/3/socialmedia#>
SELECT ?groupe ?nomGroupe WHERE {
  ?groupe a :Groupe .
  ?groupe :nomGroupe ?nomGroupe .
  FILTER NOT EXISTS {
    ?mod a :Modérateur .
    ?mod :modère ?groupe .
  }
}

requete 4: Trouver les publications avec une date:
PREFIX : <http://www.semanticweb.org/administrator/ontologies/2025/3/socialmedia#>
SELECT ?publication ?contenu ?datePubli WHERE {
    ?publication a ?type .
    VALUES ?type { :Article :Image :Video }  # Ajoute ici tes sous-classes de Publication
    ?publication :contenu ?contenu .
    ?publication :datePublication ?datePubli .
}
