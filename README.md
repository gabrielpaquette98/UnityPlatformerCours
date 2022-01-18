# UnityPlatformer - Cours Unity pour débutants par Poly Games

## Introduction
Pour commencer avec Unity et faire un projet initial, je suggère fortement d'utiliser le Unity Hub. Ce projet a été créé initialement avec la version 2021.1.17f1. Quand vous faites "New Project", vous pouvez sélectionner le template "3D" et faire "Create Project". 

#### Interface
Unity permet de déplacer les fenêtres pour obtenir une configuration adaptée à vos besoins. Vous pouvez cliquer sur le nom de la fenêtre et la glisser où vous voulez. 
 - La fenêtre « Scene » permet de visualiser la scène, c'est-à-dire le niveau, ainsi que tous les objets contenus dans le niveau, qui sont appelés des GameObjects. En maintenant le bouton droit de la souris, vous pouvez tourner la caméra sur son propre axe et déplacer la caméra avec W, A, S, D. Vous pouvez également cliquer sur les objets dans la scène pour les sélectionner et les déplacer avec les flèches. Avec les outils que vous pouvez sélectionner en haut à gauche de l'éditeur, vous pouvez soit vous déplacer dans la scène avec la main, déplacer des objets avec les flèches, tourner les objets ou changer la mise à l'échelle des objets.
 - La fenêtre « Hierarchy » permet de voir les GameObjects présent dans la scène. On peut y voir les objets et les relations entre les objets. Pour faire en sorte qu'un objet soit "enfant" d'un autre objet, vous pouvez le cliquer, le maintenir et le glisser sur un autre objet. L'objet enfant sera maintenant déplacé en même temps que son objet parent, et si l'objet parent est détruit, tous les objets enfants seront détruits. Vous pouvez sélectionner un ou des objets et vous pouvez faire un clic droit dans la hiérarchie pour manipuler les objets sélectionnés ou créer un nouvel objet.
 - La fenêtre « Game » permet de voir ce qui sera affiché au joueur lors de l'exécution du jeu. Le bouton "Play" en haut au milieu de l'éditeur permet de démarrer le jeu. Vous pouvez cliquer à nouveau sur le bouton pour désactiver l'exécution du jeu, ou cliquer sur le bouton "Pause" pour interrompre l'exécution. Le troisième bouton permet de poursuivre l'exécution pour seulement une trame.
 - La fenêtre « Inspector » permet de modifier les paramètres d'un GameObject sélectionné dans la hiérarchie. Un GameObject est essentiellement un regroupement de "Components", ou de "composantes". Chaque composante possède des attributs qui peuvent être changés, et chaque GameObject possède par défaut la composante Transform, qui représente la position, la rotation et l'échelle de l'objet. Lorsque vous créez un objet autrement qu'avec un clic droit suivi de "Create Empty", vous créez un objet qui vient déjà avec quelques composantes. Par exemple, si vous créez un cube, celui-ci viendra déjà avec son affichage (Mesh Renderer et Mesh Filter), et avec sa forme de collision (Box Collider). Les composantes peuvent être activées ou désactivées. Par exemple, si un objet doit, à un certain moment, perdre sa tangibilité, alors il est possible par divers moyens de désactiver seulement la composante du Box Collider. Dans l'éditeur, il est possible de le faire en cliquant sur le crochet visible à gauche du nom "Box Collider". Vous pouvez également créer vos propres composantes. Nous y viendrons plus tard dans ce tutoriel.
 - La fenêtre  « Project » permet de visualiser l'ensemble des Assets, c'est-à-dire les fichiers ou les ressources présentes et disponible pour votre utilisation dans le jeu, que ce soit du code, des modèles, des textures, du son ou bien d'autres. Avec un clic droit dans cette fenêtre, vous pouvez créer différents assets selon vos besoins.
D'autres fenêtres seront également pertinentes lors de ce tutoriel, comme l'Animator, l'Animation, la Console et les Project Settings. Nous y viendrons au moment où ces fenêtres seront nécessaires.

#### Boucle d'exécution
Les jeux fonctionnent avec une boucle qui s'exécute à chaque trame du jeu. Quand un niveau est chargé et lancé, une fonction d'initialisation est appelée pour chaque GameObject et pour chaque composante. À chaque trame, une fonction de mise à jour est appelée pour chaque composante de chaque GameObject présent et activé dans la scène. Cette boucle pourra être utilisée pour mettre à jour vos propres composantes, c'est-à-dire que vous pourrez implémenter du code qui sera appelé à chaque trame afin de donner vos propres comportements à des GameObjects. Il existe plusieurs fonctions qui font partie de la boucle d'exécution, mais les deux plus importantes sont Start et Update. Nous verrons en détail comment créer une composante afin d'ajouter notre propre logique au jeu dans la section suivante de ce tutoriel.

## Niveau et Joueur
Nous allons maintenant voir comment créer des objets dans la scène qui serviront de base pour un niveau, ainsi qu'un objet servant d'avatar que le joueur controlera.

#### Création du sol et d'objets
L'espace est présentement vide, sauf pour une caméra et une lumière. Pour créer un sol de base servant à implémenter la suite du prototype, vous pouvez faire un clic droit dans la hiérarchie, faire 3D Object, puis Plane. Vous pouvez nommer le plan "Ground", et dans la fenêtre d'inspecteur, vous pouvez changer le Scale pour 5, 1, 5, ce qui fera un plan suffisamment grand pour implémenter le déplacement. Le plan possède déjà les composantes requises, c'est-à-dire un Mesh Renderer et un Mesh Collider. Dans la hiérarchie, vous pouvez créer un objet 3D "Capsule" qui servira d'avatar temporaire pour le joueur. Vous pouvez placer le joueur légèrement en haut du plan, et lorsque le jeu sera exécuté, il tombera sur le plan. Pour qu'il soit affecté par le système de physique de Unity, il faut ajouter au joueur la composante "Rigidbody". Vous pouvez ajouter n'importe quelle composante à n'importe que GameObject en sélectionnant le GameObject dans la hiérarchie, et puis en sélectionnant le bouton Add Component dans l'inspecteur et en cherchant "Rigidbody". Puisque le plan n'a pas de Rigidbody, celui-ci ne peut pas tomber, alors que le joueur tombe et entre en collision avec le plan.

#### Déplacement de base
Pour faire en sorte que le joueur puisse se déplacer avec les touches du clavier, il faut créer une composante. Pour commencer, vous pouvez sélectionner l'objet qui représente le joueur, aller dans l'inspecteur et faire "Add Component". Cette fois-ci, vous pouvez écrire "PlayerMovement" et faire New Script pour créer le script C# qui contiendra le code de la composante que nous allons créer. Le nouveau script est maintenant ajouté au projet, vous pouvez aller dans la fenêtre Project, puis trouver votre nouvelle composante et la double cliquer pour que le script s'ouvre dans Visual Studio. Vous pouvez égalquement double cliquer sur le nom du script dans l'inspecteur pour l'ouvrir. Dans le script, il y a les deux fonctions de base, Start et Update. Vous pouvez faire une nouvelle fonction, GetInputs, que vous pouvez appeler dans Update. L'idée derrière cette fonction, c'est de récupérer toutes les entrées nécessaires aux déplacements du joueur pour la trame actuelle, que ce soit une entrée au clavier ou une information du monde qui nous sera importante. Pour l'instant, la fonction GetInputs devra ressembler à ceci: 

```
    private void GetInputs()
    {
        inputVector = new Vector2(Input.GetAxis("Horizontal"), Input.GetAxis("Vertical"));
        inputVector.Normalize();
    }
```

Cette fonction récupère deux Axes d'Input. Ces axes sont configurés par défauts mais vous pouvez les configurer vous-mêmes dans Edit/Project Settings/Input Manager. Le nom de l'axe à récupérer est important, car il doit être écrit exactement dans la fonction GetAxis. Un axe a une valeur qui peut varier entre -1 et 1. Au repos, l'axe est à 0, il peut y avoir un bouton négatif pour faire graduellement changer la valeur jusqu'à -1, et un bouton positif pour faire graduellement changer la valeur jusqu'à 1. Dans le cas de l'axe Horizontal et Vertical, ceux-ci devraient déjà être configurés correctement par défaut. Une fois récupéré, les deux valeurs sont mises dans un Vector2, composé de deux floats, qui serviront d'entrées pour le déplacement du joueur. Le vecteur est ensuite normalisé afin que, même si le déplacement soit à la fois vertical et horizontal, la norme du vecteur d'input soit toujours de 1. 

Nous avons vu comment récupérer les valeurs du clavier et les mettre dans un vecteur, mais maintenant il faut utiliser ces valeurs afin de causer un déplacement du joueur. Ceci peut être accompli de plusieurs manières, mais pour déplacer le joueur, ce sera fait en calculant soi-même une vélocité que nous utiliserons pour modifier la position du joueur. D'autres manières sont également valides, mais celle-ci permet un bon niveau de contrôle sur le déplacement du joueur.

```
private void FixedUpdate()
    {
        float verticalVelocity = velocity.y;
        velocity = CalculateVelocity();
        velocity.y = verticalVelocity;
        Vector3 movement = velocity * Time.deltaTime;

        Body.MovePosition(transform.position + movement);
    }
```

Vous pouvez consulter le code dans ce repo afin de voir comment est implémenté la fonction CalculateVelocity. Dans la fonction Update, après le GetInput, il faut mettre à jour une "targetVelocity", que vous pourriez utiliser directement en tant que velocity dans le calcul du mouvement de FixedUpdate, mais en l'utilisant ainsi, le déplacement devient instantané. Il faut une certaine accélération de la vélocité actuelle jusqu'à celle voulu, soit la targetVelocity, pour que le mouvement ne soit pas aussi soudain. En regardant le code fourni, vous avez surement remarqué que certaines variables possèdent un attribut ```[SerializeField]``` devant certaines variables. L'utilité de cet attribut est qu'il permet d'exposer la variable dans l'éditeur. En d'autres termes, avec cet attribut, vous pouvez modifier la valeur directement dans l'inspecteur au lieu de modifier la valeur dans le code, ce qui est très utile pour modifier la valeur pendant l'exécution pour trouver la meilleure valeur, ou encore pour avoir plusieurs objets avec la composante et donner des valeurs différentes, comme des ennemis qui auraient des quantitées de points de vie différentes mais qui utilisent le même script. C'est également pratique pour des Game Designers afin qu'ils puissent ajuster les valeurs dans l'éditeur au lieu de devoir consulter le code. Si vous ajoutez les fonctions et les variables nécessaires, votre joueur devrait maintenant tomber vers le sol et être mobile lorsque vous pesez sur les touches W, A, S, D.


