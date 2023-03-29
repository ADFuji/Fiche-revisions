# Développement objet C++

## Qu'est-ce que le développement objet ?
Le développement objet est un paradigme de programmation qui permet de modéliser des objets du monde réel. Il permet de définir des classes d'objets et de créer des instances de ces classes. Ces instances sont des objets qui possèdent des attributs et des méthodes. Les attributs sont des variables qui décrivent l'objet et les méthodes sont des fonctions qui permettent de manipuler l'objet.

### Exemple
Voici un exemple de classe `Personne` qui représente une personne. Cette classe possède deux attributs : `nom` et `age` et une méthode `afficher()` qui affiche le nom et l'âge de la personne.

    class Personne {
        private:
            string nom;
            int age;
        public:
            Personne(string nom, int age) {
                this->nom = nom;
                this->age = age;
            }
            void afficher() {
                cout << "Nom : " << nom << endl;
                cout << "Age : " << age << endl;
            }
    };

    int main() {
        Personne p("Jean", 20);
        p.afficher();
    }

## Qu'est-ce que l'héritage ?
L'héritage permet de définir une classe qui hérite des attributs et des méthodes d'une autre classe. La classe héritée est appelée classe parente et la classe qui hérite est appelée classe fille. La classe fille peut redéfinir les attributs et les méthodes de la classe parente.

### Exemple
Voici un exemple de classe `Etudiant` qui hérite de la classe `Personne`. La classe `Etudiant` redéfinit la méthode `afficher()` pour afficher le nom, l'âge et le numéro d'étudiant de l'étudiant.

    class Etudiant : public Personne {
        private:
            int numEtudiant;
        public:
            Etudiant(string nom, int age, int numEtudiant) : Personne(nom, age) {
                this->numEtudiant = numEtudiant;
            }
            void afficher() {
                Personne::afficher();
                cout << "Numéro d'étudiant : " << numEtudiant << endl;
            }
    };

    int main() {
        Etudiant e("Jean", 20, 123456);
        e.afficher();
    }

## Qu'est-ce que la polymorphisme ?
Le polymorphisme permet de définir une méthode dans une classe parente qui sera redéfinie dans une classe fille. Lors de l'exécution, la méthode redéfinie sera appelée.

Il est préférable de déclarer la méthode dans la classe parente comme `virtual` pour indiquer que la méthode sera redéfinie dans une classe fille. Si la méthode n'est pas déclarée comme `virtual`, la méthode de la classe parente sera appelée.

C'est plus propre et correspond mieux avec le principe de programmation orientée objet.

### Exemple
Voici un exemple de classe `Personne` qui possède une méthode `afficher()` qui affiche le nom et l'âge de la personne. La classe `Etudiant` redéfinit la méthode `afficher()` pour afficher le nom, l'âge et le numéro d'étudiant de l'étudiant.

    class Personne {
        private:
            string nom;
            int age;
        public:
            Personne(string nom, int age) {
                this->nom = nom;
                this->age = age;
            }
            virtual void afficher() {
                cout << "Nom : " << nom << endl;
                cout << "Age : " << age << endl;
            }
    };

    class Etudiant : public Personne {
        private:
            int numEtudiant;
        public:
            Etudiant(string nom, int age, int numEtudiant) : Personne(nom, age) {
                this->numEtudiant = numEtudiant;
            }
            void afficher() {
                Personne::afficher();
                cout << "Numéro d'étudiant : " << numEtudiant << endl;
            }
    };

    int main() {
        Personne *p = new Etudiant("Jean", 20, 123456);
        p->afficher();
    }

## Qu'est-ce que le virtuel pur ?
Le virtuel pur permet de définir une méthode dans une classe parente qui sera redéfinie dans une classe fille. La classe parente ne peut pas être instanciée car elle contient une méthode virtuelle pure.

Traduction : la classe parente ne peut pas être instanciée car elle n'est pas tangible, elle ne peut pas être représentée par un objet.

### Exemple

    class Affichable {
        public:
            virtual void afficher() = 0;
    };

    class Personne : public Affichable {
        private:
            string nom;
            int age;
        public:
            Personne(string nom, int age) {
                this->nom = nom;
                this->age = age;
            }
            void afficher() {
                cout << "Nom : " << nom << endl;
                cout << "Age : " << age << endl;
            }
    };

    int main() {
        Affichable *a = new Personne("Jean", 20);
        a->afficher();
    }

# /!\ ATTENTION /!\
Une classe fille ne peut pas redéfinir une méthode virtuelle pure de la classe parente. Elle doit redéfinir la méthode virtuelle pure de la classe parente.

De plus, son destructeur doit être déclaré comme `virtual` pour que le destructeur de la classe fille soit appelé lors de la destruction de l'objet.

## Lecture d'un UMl
# /!\ LISEZ LE COURS POUR COMPRENDRE CE QUI SUIT /!\<br>
Un diagramme UML est un diagramme qui permet de représenter comment les classes sont liées entre elles. Il permet de représenter les classes, les attributs, les méthodes, les relations entre les classes, etc.

### Signification des symboles
- `+` : public
- `-` : private
- `#` : protected
### Signification des relations
- `--` : héritage
- `<>` : association
- `<>--` : association avec héritage
- `*` : composition
- `*--` : composition avec héritage
- `o` : dépendance
- `o--` : dépendance avec héritage
### Exprimer les types de retour et les paramètres
- `: type` : type de retour
- `(type)` : paramètre
- `(type1, type2, ...)` : paramètres
### Exemple
Voici un exemple de diagramme UML qui représente les classes `Personne`, `Etudiant` et `Professeur`.

    class Personne {
        -nom : string
        -age : int
        +Personne(nom : string, age : int)
        +afficher()
    }

    class Etudiant {
        -numEtudiant : int
        +Etudiant(nom : string, age : int, numEtudiant : int)
        +afficher()
    }

    class Professeur {
        -numProfesseur : int
        +Professeur(nom : string, age : int, numProfesseur : int)
        +afficher()
    }

    Personne <|-- Etudiant
    Personne <|-- Professeur

## Différents types de pointeurs
### Pointeur simple
Un pointeur simple est un pointeur qui pointe vers une variable. Il est déclaré comme suit :

    type *nom;

### Unique_ptr
Un unique_ptr est un pointeur qui pointe vers une variable, mais qui ne peut être utilisé qu'une seule fois. Il est déclaré comme suit :

    unique_ptr<type> nom;

### Shared_ptr
Un shared_ptr est un pointeur qui pointe vers une variable, mais qui peut être utilisé plusieurs fois. Il est déclaré comme suit :

    shared_ptr<type> nom;

### Smart_ptr
Un smart_ptr est un pointeur qui pointe vers une variable, mais qui peut être utilisé plusieurs fois. Si le pointeur est utilisé plusieurs fois, il sera détruit automatiquement lorsqu'il ne sera plus utilisé. Il est déclaré comme suit :

    smart_ptr<type> nom;

