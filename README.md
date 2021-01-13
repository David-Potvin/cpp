
- [Le destructeur](#le-destructeur)
- [Methode constante](#methode-constante)
- [pointeur this](#pointeur-this)
- [constructeur de copie](#constructeur-de-copie)
- [Heritage](#heritage)
- [portee protected](#portee-protected)
- [methode virtuelle](#methode-virtuelle)
- [methode virtuelles pures](#methode-virtuelles-pures)
- [classes abstraites](#classes-abstraites)
- [methode statique](#methode-statique)
- [attribut statique](#attribut-statique)
- [amitie](#amitie)
### Le destructeur
Le destructeur permet de desallouer la memoire lorsqu'on fait une allocation dynamique 
```
// si j'ai cette ligne dans mon constructeur
int *p = new MonObjet();

// il me faudra cette ligne dans mon destructeur
delete p;
```

### Methode constante
la methode constante indique au programmeur que les arguments ne seront pas modifiees (read-only)
```
void maMethode(int &objet) const;
```
Ce type de methode peut etre utilise pour creer des accesseurs.

note : ce n'est pas obligatoire d'utiliser une methode constante mais cela aide les programmeurs car "code is more often read than written". 
### pointeur this
Toute classe dispose d'un pointeur this et il pointe vers l'objet lui-meme
### constructeur de copie
C'est une surcharge du constructeur qui prend une reference constante de l'objet de meme type.

Il sert a copier les attributs d'un objet dans un autre.
```
class Robot
{
    public:
        Robot(Robot const&); // constructeur de copie
};
```
note : un constructeur de copie est **generer automatiquement**, mais il se contente de copier les attributs. Cela peut etre **problematique** si certains attributs sont des pointeurs.

note : si on doit ecrire un constructeur de copie, il faut **obligatoirement** ecrire une surcharge de l'**operateur=**.

### Heritage
Permet de creer une classe a partir de classes deja existantes.

Si on peut dire qu'un objet A est un objet B, on peut faire en sorte que A herite de B.

Par exemple: un humain est un vivant.

Quand une classe herite d'une autre, elle herite des methodes et des attributs de cette dernier. Il est cependant possible de les redefinir (on parle alors de masquage).

```
Vivant *vivant(0);
Humain *humain = new Humain();

vivant = humain;
```

En haut, on ***dirige le pointeur vers la partie fille qui a ete heritee.*** 
Ce n'est pas equivalent a dire qu'on attribue l'enfant au parent.

Il est possible d'utiliser l'un des constructeurs d'une classe parent dans la classe enfant afin d'initialiser des parametres

```
Humain::Humain() : Vivant(), profession("pompier")
{

}
```
### portee protected
Les elements de cette portee sont ne sont pas accessible depuis l'exterieur, sauf si c'est une classe fille. 

Cela nous evite de creer une panoplie d'accesseurs. 

C'est une portee qui se trouve entre public et private en terme de restriction 

Utiliser cette porte a seulement du sens quand on utilise l'heritage

### methode virtuelle
Les méthodes virtuelles pures sont destinées à être définies dans les classes dérivées. 

### methode virtuelles pures
Il faut ajouter = 0 a la fin du prototype de la methode.

Si on declare ce type de fonction dans une classe et que d'autres classes heritent de cette classe, les classes enfant auront tous cette fonction, **mais pas la classe parent**.

```
class Vivant 
{
    public:
        virtual int nbrAnnee() const = 0; 
};
```

Ici, toute les classes qui heritent de Vivant pourront utiliser nbrAnnee(), mais va les objets de type Vivant.

### classes abstraites
c'est un type de classe qui ne peut pas etre instancier et qui a au moins une methode virtuelle pure.

**Toute classe heritant d'une classe abstraite doit ses methodes virtuelles pures.**

une methode virtuelle ***peut*** etre redefinie dans une classe fille
une methode virtuelle pure ***doit*** etre redefinie dans une classe fille

### methode statique
type de methode appartenant a une classe, **mais pas aux objets instanciees**

```
// fichier .h
class Vivant
{
    public:
        static void maMethode();
};

---------------------------------
// fichier .cpp
// static n'est pas dans le fichier .cpp
void Vivant::maMethode()
{
    
}
```

On peut utiliser ces methodes sans instancier un objet de la classe.

note: ce type de methode ne peut pas utiliser les attributs de la classe.

### attribut statique
un attribut statique est accessible depuis l'exterieur, mais si sa portee est private ou protected.

note : l'initialisation de l'attribut statique se fait dans l'espace global (pas le constructeur, ni dans le main).

Ce type d'attribut se comporte comme une variable globale

On peut utiliser ce type d'attribut pour compter le nombre d'instances d'un objet.

### amitie
l'amitie est le fait de donne un access complet aux elements d'une classe

une fonction f amie de la classe Vivant, peut modifier les attributs de la classe A, ***meme si les attributs sont private ou protected***. f pourra aussi utiliser les methodes de A.

Une fonction amie ne doit pas modifier l'instance de la classe

Les fonctions amies doivent etre utilisees seulement si on ne peut pas faire autrement.
