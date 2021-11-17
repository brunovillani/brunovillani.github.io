## Modèle Data Transfer Object

*source*: [Java DTO Pattern](https://www.baeldung.com/java-dto-pattern)

L'un des principes le plus connus de la programmation est le **Single Responsibility**. Ce principe stipule qu'une classe doit avoir une seule responsabilité, donc une seule raison d'exister dans le code. Bien suivi, ce principe organise le code de façon bien lisible et tous les classes on un ensemble de méthodes et propriétés bien scopées pour accomplir ses rôles, correct ? Pas du tout ! Responsabilité n'indique pas exactement une action. Selon le *design pattern* utilisé, certaines classes peuvent être responsables pour retenir un ensemble de données dans leurs propriétés, mais pas pour les traiter. On les appelle *Data Transfer Objects* (DTO)

L'idée de la POO nous fait penser aux classes comme un modèle abstrait qui représente on objet physique. Les propriétés sont les caractéristiques et les méthodes sont les actions possibles de faire avec cet objet. Si un objet contient un autre, l'une de ses propriétés peuvent être une référence à lui. Un exemple classique serait une classe 'Voiture' avec des propriétés comme 'couleur' et 'poids' et des méthodes comme 'conduire' et 'accélérer'. Cette classe pourrait faire référence à la classe 'Moteur' pour l'utiliser dans ses méthodes.

![structure-classique](../assets/Data_Transfer_Object/image-20211116084522319.png)

<figure>Structure classique de classes et ses relations</figure>

L'exemple classique est simple à comprendre, mais ne sert pas à tous les modélisation. Un bon exemple est le processus d'achat avec une carte de crédit. La carte contient des informations mais n'exécute pas d'action et ces informations sont utilisées par tous les autres classes du processus. Nous pouvons penser aux informations de la carte comme un paquet d'informations, ou classe DTO, qui est passée aux méthodes d'autres classes. La logique s'organise donc comme un flow. Les méthodes sont appelées en séquence et ils reçoivent le DTO au besoin.

![structure-dto](../assets/Data_Transfer_Object\image-20211116084622088.png)

<figure>Flow de transmission d'un DTO</figure>

Le processus de 'flow d'information' peut rendre la logique de certaines applications très intuitive. Dans une application web, les pages ou les api peuvent démarrer leur traitement des informations avec un DTO. Une requêtes de l'api ou un 'submit' d'un bouton d'une page représentent un flow de transformation des informations. La séquence de traitements part de la méthode d'une classe d'haut niveau et fait une séquence d'appels à d'autres méthodes des classes de niveau plus basse. À la fin du traitement, les méthodes retournent d'autres informations au point de début du flow, ce qui finit le traitement.

![flow-dto](../assets/Data_Transfer_Object\image-20211116084640323.png)

<figure>Flow de traitement d'un DTO</figure>

L'un des plus grands avantages de l'utilisation du DTO est le faible couplage entre les classes de la logique. Comme le point en commun est le DTO, les autres classes peuvent utiliser des interfaces pour traiter la logique de façon plus abstraite, ayant surtout le DTO comme paramètre à transférer.

