.. _chap-tpIntroductionPython:

#########################################
Travaux pratiques - Introduction à Python
#########################################

(correspond à 1 séance de TP)

.. only:: html

    .. container:: notebook

        .. image:: _static/jupyter_logo.png
            :class: svg-inline

        `Cahier Jupyter </tpIntroductionPython.ipynb>`_

Références externes utiles :

  * `Site scikit-learn <http://scikit-learn.org/stable/index.html>`_
  * `Site du langage Python <https://www.python.org>`_
  * `Documentation de Python en français <https://docs.python.org/fr/3/>`_

Les travaux pratiques emploient le langage Python et cette première séance a pour premier objectif de vous le faire découvrir. Vous pouvez, par ailleurs, trouver de (très) nombreux tutoriels Python sur Internet, en français ou en anglais (ou d'autres langues).

Parmi les caractéristiques notables du langage Python nous pouvons mentionner :

 * langage de programmation objet où tout (ou presque) est objet ;
 * typage fort : la conformité aux types est vérifiée, les conversions implicites de type ne sont pas autorisées ;
 * typage dynamique : le type est déterminé à l'exécution, une déclaration explicite du type d'une variable n'est pas nécessaire ;
 * gestion automatique de la mémoire par un mécanisme de « ramasse-miettes » ;
 * **sensible à l'indentation** : les structures de contrôle n'emploient pas de délimiteurs (comme ``begin`` et ``end``, ou ``{`` et ``}``), tout est basé sur l'indentation (par ex. multiple de 4 espaces)
 * sensible à la casse : différence entre majuscules et minuscules.

Si vous maîtrisez déjà les bases de Python, vous pouvez aller directement à la séance `d'introduction à Scikit-learn <tpIntroductionScikitLearn>`_.

En complément de cette introduction, vous pouvez suivre le `tutoriel Python officiel en français <https://docs.python.org/fr/3/tutorial/>`_.

Python 2 ou Python 3 ?
**********************

Depuis janvier 2020, la version 2 du langage Python n'est `plus maintenue <https://www.python.org/doc/sunset-python-2/>`_. scikit-learn ayant décidé d'abandonner le support de Python 2 depuis sa version 0.20, nous emploierons et vous recommendons Python 3 dans les TP.

Interpréteur Python
*******************

Python est un langage interprété pouvant s'exécuter sur diverses plateformes. Vous pouvez par exemple

Si vous travaillez sur les machines des salles informatiques du CNAM, vous n'avez rien à faire, tout est déjà installé.

Si vous réalisez ces TP sur votre machine personnelle, vous pouvez consulter `les instructions d'installation de scikit-learn <installationScikitLearn>`_ pour installer les bons logiciels.

Il faut a minima un interpréteur Python (accessible via la commande ``python3`` dans un terminal Linux/MacOS ou une console Windows). Pour plus de confort, nous recommandons également un environnement de programmation tel que Spyder ou Jupyter.

.. Si vous êtes auditeur du CNAM, vous pouvez accéder à un serveur Jupyter en ligne en passant par `Moodle <https://lecnam.net>` (Mes enseignements > RCP 208 > Accès au notebook).

Documentation, aide en ligne de commande
****************************************

L'interpréteur Python peut vous renvoyer de la documentation et de l'aide de différentes façons.

Par exemple, définissons un couple et examinons-le. La fonction native ``print`` permet d'afficher le contenu d'une variable :

.. code-block:: python

    t = (8,9)
    print(t)

Si l'on veut savoir quelles sont les méthodes de l'objet ``t``, on peut utiliser la fonction ``dir`` :

.. code-block:: python

    dir(t)
    # Affiche ['__add__', '__class__', ... 'count', 'index']

Pour avoir plus d'explications sur ces méthodes, il est possible d'appeler la fonction ``help`` :

.. code-block:: python

    help(t)
    # Affiche :
    # Help on tuple object:
    #
    # class tuple(object)
    #  |  tuple() -> empty tuple
    #  |  tuple(iterable) -> tuple initialized from iterable's items
    #  |
    #  |  If the argument is a tuple, the return value is the same object.
    #  |
    #  |  Methods defined here:
    #  |
    #  |  __add__(self, value, /)
    #  |      Return self+value.
    #  |
    #  | ...
    #  |
    #  |  __getattribute__(self, name, /)


En ligne de commande, vous pouvez appuyer sur la touche ``Espace`` pour passer à la page suivante et sur la touche ``q`` pour quitter l'aide (comme pour la commande ``man`` de linux).

Une fois entré dans l'aide avec ``help()``, il est possible de demander une aide spécifique, par exemple d'avoir la liste des modules Python présents :

.. code-block:: python

    help()
    # help> modules
    # ...
    # help> quit

Examinez également les résultats des appels suivants (il y a bien d'autres outils d'**introspection** pour Python) :

.. code-block:: python

    print(type(t))
    # Affiche : <class 'tuple'>
    print(id(t))

Entrez

.. code-block:: python

    t = ("3","4")
    print(id(t))


.. admonition:: Question :

   Est-ce le même ``id`` que plus haut ? Que s'est-il passé ?

.. ifconfig:: tpml in ('public')

   .. admonition:: Correction :

        Non, ce n'est pas le même ``id`` car ce n'est pas le même objet. Par ``t = ("3","4")`` nous avons donné le (même) nom ``t`` à un nouvel objet, le tuple ``("3","4")``.

.. admonition:: Note

    Les lignes commençant par ``#`` sont des **commentaires**. Elles ne sont pas interprétées par Python mais servent à expliquer ou documenter le code.
    Il est possible d'écrire des commentaires multilignes en les encadrant par ``"""``.

Syntaxe
*******

L'affectation de valeurs à une variable (ou l'association d'objets à des noms) est faite en utilisant le signe ``=``. Pour la vérification de l'égalité on employe deux signes ``=`` collés, ``==``. Les commentaires sur une seule ligne commencent par ``#``, les commentaires multi-lignes commencent et se terminent par ``"""``.

Types de base
-------------

Différents types de base sont disponibles dans Python. Pour la plupart de ces types de base, dont ``bool`` (booléen), ``int`` (entier), ``float`` (réel), ``str`` (chaîne de caractères), ``tuple`` (vecteur), les « variables » qui les possèdent sont **immuables** (*immutable*) : il n'est pas possible de changer leur valeur ! En revanche, il est possible de donner le même *nom* de variable à une nouvelle donnée, comme dans l'exemple ci-dessus que nous reprenons :

.. code-block:: python

    t = (8,9)
    print(id(t))

    t = ("3","4")
    print(id(t))

Lors de ce qui ressemble à l'affectation d'une nouvelle valeur à une variable, ``t = ("3","4")``, nous avons en fait donné le même nom ``t`` à un nouvel objet ``("3","4")``, les identifiants de l'ancien ``t`` et du nouveau ``t`` sont donc naturellement différents.

.. code-block:: python

    entier = 1
    reel = 3.14
    chaine = "pi"

Un *tuple* peut être composé de données de types différents :

.. code-block:: python

    v = (entier, reel, chaine)
    print(v)
    # (1, 3.14, 'pi')
    print(type(v))
    # <class 'tuple'>

Nous remarquerons enfin que les délimiteurs d'une chaîne de caractères peuvent être soit les ``"``, soit les ``'`` ; ce qui compte c'est la cohérence entre le début et la fin de la chaîne :

.. code-block:: python

    s = "toto"
    print(s)
    # 'toto'
    s = 'toto'
    print(s)
    # 'toto'
    s = "toto' # Erreur, il faut utiliser les mêmes guillemets pour ouvrir et fermer la chaîne !!


Listes
------

Les types de base modifiables (*mutable*) sont les **listes** et les **dictionnaires**. Une liste est un tableau unidimensionnel, dont les éléments peuvent avoir des types différents (et peuvent être des listes à leur tour) ; le premier élément est identifié par l'indice ``0``, le dernier par l'indice ``-1``. Les exemples ci-dessous illustrent également l'utilisation des ``:`` pour indiquer des intervalles d'indices. Ces mêmes règles concernant les indices sont valables pour les tuples.

.. code-block:: python

    liste = [entier, reel, chaine]
    print(liste)
    # [1, 3.14, 'pi']
    print(type(liste))
    # <class 'list'>
    print(liste[0])
    # 1
    print(liste[2])
    # 'pi'
    print(liste[3]) # Erreur !

Les indices négatifs permettent d'accéder aux éléments en commençant par la fin de la liste :

.. code-block:: python

    print(liste[-1])
    # 'pi'
    print(liste[-2])
    # 3.14


Le symbole ``:`` permet d'effectuer du *slicing*, c'est-à-dire de découper des sous-listes :

.. code-block:: python

    print(liste[:1]) # Extrait la sous-liste de tous les éléments jusqu'à 1 (exclu)
    # [1]
    print(liste[:2]) # Extrait la sous-liste de tous les éléments jusqu'à 2 (exclu)
    # [1, 3.14]

    print(liste[:-1]) # Extrait la sous-liste jusqu'au dernier élément (exclu)
    # [1, 3.14]
    print(liste[:3])
    # [1, 3.14, 'pi']
    print(liste[0:]) # Extrait la sous-liste à partir du premier élément (inclus)
    # [1, 3.14, 'pi']
    print(liste[1:]) # Extrait la sous-liste à partir du deuxième élément (inclus)
    # [3.14, 'pi']

Les listes disposent de plusieurs méthodes utiles (regardez-les avec ``help(liste)``), parmi lesquelles :

.. code-block:: python

    # Concaténation de listes
    print(liste + liste)
    # [1, 3.14, 'pi', 1, 3.14, 'pi']

.. code-block:: python

    # Longueur d'une liste
    len(liste)

.. code-block:: python

    # Minimum et maximum d'une liste
    print(min([3, 10, 1, 5, 24]))
    print(max([1.24, -12.0, 5.99]))

    # Attention, erreur si les éléments ne sont pas comparables :
    print(min(['pi', '12', 3, 1]))
    # Traceback (most recent call last):
    #   File "<stdin>", line 1, in <module>
    # TypeError: '<' not supported between instances of 'int' and 'str'

.. code-block:: python

    # Nombre d'occurrences d'un élément dans une liste
    liste = [3.14, 12, 0, 3.14, 9, 3.14, 7]
    liste.count(3.14)


.. code-block:: python

    # Tri d'une liste en ordre croissant
    liste.sort()
    print(liste)

.. code-block:: python

    # Suppression d'un élément de la liste
    del liste[1]
    print(liste)


.. code-block:: python

    # Cherche la position de l'élément dans la liste
    print(liste.index(3.14))
    # 1
    print(liste.index(9))
    # 4

.. code-block:: python

    # Renverse une liste
    liste.reverse()
    print(liste)
    # [12, 9, 7, 3.14, 3.14, 0]


Dictionnaires
-------------

Les dictionnaires sont des tableaux associatifs, autrement dit des ensembles de paires ``{clé : valeur}``, par exemple :

.. code-block:: python

    cours = { 'RCP208' : 2016, 'RCP209' : 2017, 'RCP216' : 2017 }
    print(cours)
    # {'RCP216': 2017, 'RCP208': 2016, 'RCP209': 2017}
    print(cours['RCP209'])
    # 2017
    cours['RCP210']  # Erreur ! La clé n'existe pas
    # Traceback (most recent call last):
    #  File "<stdin>", line 1, in <module>
    # KeyError: 'RCP210'

Il est possible de mélanger les types dans un dictionnaire (dans les clés et dans les valeurs), ainsi que d'avoir des valeurs qui sont des tuples ou des listes (ou des listes de listes, etc.) :

.. code-block:: python

    dico = { 1 : 'toto', 'titi' : 10, 1000 : (1,2,3) }

.. code-block:: python

    dico = { 1 : 'toto', 'titi' : 10, 1000 : [(1,2,3),['A','b']]}

Plusieurs méthodes spécifiques aux dictionnaires peuvent être utiles, par exemple :

.. code-block:: python

    # Obtenir les clés du dictionnaire
    print(dico.keys())
    # dict_keys(['titi', 1, 1000])
    # Obtenir les valeurs du dictionnaire
    print(dico.values())
    # dict_values([10, 'toto', [(1, 2, 3), ['A', 'b']]])
    # Obtenir les paires (clé, valeur)
    print(dico.items())
    # dict_items([('titi', 10), (1, 'toto'), (1000, [(1, 2, 3), ['A', 'b']])])

.. admonition:: Question :

   Que retourne chacune de ces méthodes ?

.. ifconfig:: tpml in ('public')

    .. admonition:: Correction

        ``.keys()`` renvoie les clés du dictionnaires tandis que ``.values()`` renvoie ses valeurs.
        ``.items()`` renvoie une liste de paires (clé, valeur).

Pour tenter de clarifier la différence entre ce qui est immuable et ce qui est modifiable, prenons l'exemple suivant :

.. code-block:: python

    valeur = 1
    liste = []
    print(liste)
    # []
    liste.append(valeur)
    print(liste)
    # [1]
    meme_liste = liste
    print(meme_liste)
    # [1]
    meme_liste.append(3)
    valeur = 2
    print(valeur)
    # 2
    print(liste)
    # [1, 3]
    print(meme_liste)
    # [1, 3]

Comment expliquer les résultats ? Rappelons d'abord que les « variables » de type ``int`` sont immuables, alors que celles de type ``list`` sont modifiables.

Dans la première ligne (``valeur = 1``), une association est faite entre le *nom* ``valeur`` et un objet qui est l'entier ``1``. La seconde ligne (``liste = []``) fait une association entre le nom ``liste`` et un objet qui est une liste vide. L'appel de la méthode ``append`` dans ``liste.append(valeur)`` modifie cet objet liste vide en lui ajoutant l'objet désigné par le nom ``valeur``. Dans ``meme_liste = liste`` on ajoute un nouveau nom pour l'objet désigné par ``liste``.

L'appel ``meme_liste.append(3)`` modifie l'objet désigné par ``meme_liste`` (et aussi par ``liste``) en lui ajoutant l'objet ``3`` (un entier). Avec ``valeur = 2``, le nom ``valeur`` n'est plus associé à l'objet auquel il était associé avant (un entier ``1``) mais à un nouvel objet (un entier ``2``) ; cela ne peut avoir d'impact sur l'objet désigné par ``liste`` ou ``meme_liste``, qui est une liste (vide au départ, ensuite un objet ``1`` lui a été ajouté, et enfin un objet ``3``).

Ceci devrait permettre de comprendre aussi le passage de paramètres aux :ref:`fonctions`.

Structures de contrôle
**********************

Pour le contrôle de l'exécution d'un programme il est possible d'utiliser les tests de conditions avec ``if`` / ``elif`` / ``else`` et les boucles ``for`` ou ``while``. Remarquer l'utilisation de ``:`` avant les lignes qui exigent un niveau d'indentation supérieur (et **obligatoire** !).

Les boucles ``for`` permettent de parcourir n'importe quel itérable, typiquement des listes :

.. code-block:: python

    liste = range(6)

    for valeur in liste:
        if valeur in [0, 2, 4]:
            # "break" quitte la boucle sans considérer "else"
            # "continue" démarre l'itération suivante
            continue
        else:
            print(valeur,' : impaire')

    #1  : impaire
    #3  : impaire
    #5  : impaire

Les boucles ``while`` s'exécutent tant qu'une condition est vérifiée :

.. code-block:: python

    i = 5
    while i > 0:
            print(i)
            i = i-1


Il n'y a pas d'équivalent de ``switch`` en Python, il faut employer ``if`` / ``elif`` / ``else`` :

.. code-block:: python

    if liste[1] == 0:
        print('liste[1] est 0')
    elif liste[1] == 1:
        print('liste[1] est 1')
    else:
        print('?')

Création et manipulation de listes avec la `compréhension de liste <https://docs.python.org/fr/3/tutorial/datastructures.html#list-comprehensions>`_ (*list comprehension*) :

.. code-block:: python

    l1 = [1, 2]
    l2 = [1, 2, 3]
    [x * y for x in l1 for y in l2]

Forme équivalente :

.. code-block:: python

    print([x * y for x in l1 for y in l2])
    # [1, 2, 3, 2, 4, 6]

Autres exemples :

.. code-block:: python

    print([x * y for x in l1 if x > 1 for y in l2])
    # [2, 4, 6]
    print(any([i % 3 for i in [x * y for x in l1 for y in l2]]))
    # True

.. admonition:: Question :

   Expliquez ce que fait chacun de ces exemples.

.. ifconfig:: tpml in ('public')

   .. admonition:: Correction :

        Pour ``[x * y for x in l1 for y in l2]`` : produit une liste composée des produits des valeurs de la liste ``l1`` avec les valeurs de la liste ``l2``, la liste parcurue en premier étant ``l2`` (résultat ``[1, 2, 3, 2, 4, 6]``).

        Pour ``[x * y for x in l1 if x > 1 for y in l2]`` : seules sont considérées les valeurs supérieures à 1 dans ``l1``.

        Pour ``any([i % 3 for i in [x * y for x in l1 for y in l2]])`` : y a-t-il au moins un élément de la liste résultat de ``[x * y ... ]`` qui ne soit pas divisible par 3 (reste de la division par 3, c'est à dire ``i % 3``, non nul) ?

.. admonition:: Question :

    À partir des listes suivantes de mois et respectivement de nombres de jours correspondants, construisez un dictionnaire qui associe à chaque mois son nombre de jours (années non bisextiles).

    .. code-block:: python

        mois = ['janvier','février','mars','avril','mai','juin','juillet','août','septembre','octobre','novembre','décembre']
        nbJours = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]


.. ifconfig:: tpml in ('private')

    .. only:: jupyter

        .. code-block:: python


.. ifconfig:: tpml in ('public')

    .. admonition:: Correction :

        De la même façon que dans les exemples avec listes, on crée un dictionnaire (``{}`` au lieu de ``[]``) composé de paires ``mois[i] : nbJours[i]`` :

        .. code-block:: python

            dico = {mois[i] : nbJours[i] for i in range(0,11)}


.. _fonctions:

Fonctions, fonctions anonymes
*****************************

La définition d'une fonction commence par ``def``. Une fonction peut avoir zéro, un ou plusieurs arguments. Les arguments optionnels possèdent des valeurs par défaut. Une fonction peut retourner une valeur (ou un tuple, donc plusieurs valeurs) avec ``return`` ou non.

Le premier exemple ci-dessous devrait aider à comprendre la transmission des paramètres :

.. code-block:: python

    def fonction(immuable, modifiable, optionnel='valeur par défaut'):
        immuable = 'new'
        modifiable.append(4)
        print(immuable, modifiable, optionnel)

    chaine1 = 'old'
    liste = [1, 2]
    chaine2 = 'nouvelle valeur'
    fonction(chaine1, liste, chaine2)
    # new [1, 2, 4] nouvelle valeur

Notre variable ``liste`` a été modifiée à l'intérieur de la fonction mais pas la variable ``chaine1`` car les chaînes de caractère sont immuables :

.. code-block:: python

    print(liste)
    # [1, 2, 4]
    print(chaine1)
    # 'old'
    fonction(chaine1, liste)
    # new [1, 2, 4, 4] valeur par défaut

L'utilisation de ``print`` plutôt que l'appel direct permet de voir que la fonction ne retourne rien (``None``) :

.. code-block:: python

    print(fonction(chaine1, liste, chaine2))
    # new [1, 2, 4, 4, 4] nouvelle valeur
    # None

Ici, ``liste`` est un nom associé à un objet liste, donc modifiable ; à chaque appel, la fonction ajoute un élément à cet objet. Le nom ``chaine1`` est associé à un objet de type chaîne de caractères, donc immuable ; dans la fonction, le nom ``chaine1`` est **localement** associé à un nouvel objet, la chaîne ``'new'``, mais cela n'a pas d'impact sur l'association de ``chaine1`` à l'objet ``'old'`` à l'extérieur de la fonction.

L'exemple suivant montre une fonction qui retourne un tuple :

.. code-block:: python

    def fonction2(immuable, modifiable, optionnel='valeur par défaut'):
        immuable = 'new'
        modifiable.append(4)
        return immuable, modifiable, optionnel

    chaine1 = 'old'
    liste = [1, 2]
    chaine2 = 'nouvelle valeur'
    print(fonction2(chaine1, liste, chaine2))
    # ('new', [1, 2, 4], 'nouvelle valeur')

Les fonctions lambda ou `fonctions anonymes <https://docs.python.org/fr/3/tutorial/controlflow.html#lambda-expressions>`_ comportent une seule instruction, par exemple :

.. code-block:: python

    fAdHoc = lambda x, y: x + y
    print(fAdHoc(2,3))
    # 5

Cette définition est une forme abrégée de

.. code-block:: python

    def fAdHoc(x, y): return(x + y)

Il n'est pas indispensable de donner un nom à une fonction lambda :

.. code-block:: python

    (lambda x, y: x + y)(4,6)
    # 10

Une fonction lambda sans nom est qualifiée d'anonyme.

Exceptions
**********

Python propose un traitement standard des exceptions. L'exemple suivant indique la syntaxe à employer.

.. code-block:: python

    def autreFonction(n):
            try:  # instruction susceptible de lever une exception
                print(1 / n)
            except ZeroDivisionError:  # si l'exception est levée
                print('Division par 0 !')
            else:  # sinon
                pass
            finally:
                # exécuté après le bloc "try" et le
                #  traitement des éventuelles erreurs
                print('    fini...')

    autreFonction(1)
    autreFonction(0)

Classes et héritage
*******************

Il est utile mais pas indispensable de bien connaître la programmation objet pour bien suivre les travaux pratiques, ou pour faire le projet de l'UE RCP209.

En Python, on peut définir des variables partagées par toutes les instances d'une classe. Aussi, l'héritage multiple est possible. La définition d'une classe a la forme suivante (n'entrez pas ceci dans l'interpréteur Python, ce n'est pas une définition complète) :

.. code-block:: python

    class NouvelleClasse():
        attribut_de_classe = ...

        def __init__(self):  # constructeur
            # ...
            pass

        def methode(self, arg1, arg2, arg3):  # methode de l'objet
            # ...
            pass

        # ...

    class NouvelleClasseHeritage(NouvelleClasse):

        # ...
        pass

Création d'une nouvelle instance de la classe :

.. code-block:: python

    instanceNouvelleClasse = NouvelleClasse()


Entrées et sorties
******************

La fonction native ``open`` permet d'ouvrir un flux de données depuis un fichier.

Cette fonction prend deux arguments : un chemin vers le fichier et le mode de lecture (lecture, écriture, binaire, etc.).

Exemple d'accès à un fichier texte :

.. code-block:: python

    # Ouverture du fichier en mode écriture ('w' pour 'write')
    fichierTexte = open('texte.txt', 'w')
    fichierTexte.write('Mon texte à moi\n')
    fichierTexte.close()

    # Ouverture du fichier en mode lecture
    fichierTexte = open('texte.txt')
    print(fichierTexte.read())
    # Mon texte à moi
    fichierTexte.close()


L'instruction ``with`` permet de ne pas avoir à fermer manuellement le fichier en utilisant un `gestionnaire de contexte <https://docs.python.org/fr/3/reference/compound_stmts.html?highlight=with#the-with-statement>`_.

.. code-block:: python

    # le mode 'a' permet d'ajouter des lignes sans écraser le fichier ('append')
    with open('texte.txt', 'a') as fichierTexte:
        fichierTexte.write('Et une ligne de plus\n')


    with open('texte.txt') as fichierTexte:
        print(fichierTexte.read())
        # Mon texte à moi
        # Et une ligne de plus

Dans ces exemples, les fichiers sont ouverts dans le répertoire dans lequel Python a été lancé. Il est possible de spécifier le chemin avant le nom du fichier.

.. admonition:: Question :

   Quelle conséquence a la suppression du second argument de la fonction ``open`` ?

.. ifconfig:: tpml in ('public')

   .. admonition:: Correction :

        C'est la valeur ``'r'`` qui est utilisée par défaut.


Enfin, le module ``pickle`` permet de stocker des objets Python dans des fichiers binaires et de les lire.

Utilisation d'un fichier binaire pour enregistrer ou lire des données/objets quelconques :

.. code-block:: python

    import pickle
    liste = [1, 3.14, 'pi']
    fichierBinaire = open('bin.dat', 'wb')
    pickle.dump(liste, fichierBinaire)
    fichierBinaire.close()

    fichierBinaire = open('bin.dat', 'rb')
    listeIdentique = pickle.load(fichierBinaire)
    print(listeIdentique)
    # [1, 3.14, 'pi']

Nous allons ensuite approfondir cette introduction en explorant les bibliothèques `Numpy, Scipy, MatPlotLib et Scikit-learn <tpIntroductionScikitLearn.html>`_.