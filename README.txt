Réseaux et Internet
 Performance TCP 
Description du Projet

Dans ce projet vous devez étudier la performance d'un émetteur TCP du point de vue du débit.

Pour commencer, vous devez donc estimer le débit des connexions TCP, à l'aide d'un programme C qui :
lira un fichier .pcap contenant des paquets capturés avec le logiciel Tcpdump ou Wireshark
vérifiera la présence de paquets TCP
Pour chaque flux TCP produira un fichier texte th-flowid.txt (où flowid correspond à l'identifiant TCP du flux en question), qui contiendra 2 colonnes : une colonne temps, une colonne débit

Le débit sera calculé sur des intervalles régulier d'une seconde et le débit correspondant à chaque intervalle de temps sera donné en Kilobits par second (Kbps). Notez que le débit TCP sera calculé uniquement en fonction de la charge utile de chaque paquet. Enfin, à l'aide de n'importe quel outil, vous produirez une image à partir du fichier texte, qui montrera graphiquement l'évolution du débit.

Une fois ayant créé votre programme C, vous pouvez procéder à la campagne de test dans laquelle, vous devez télécharger des donnée depuis le serveur de votre choix (en veillant à ce que le temps de téléchargement dépasse au moins la vingtaine de secondes), tandis que le trafique réseau est enregistré par tcpdump.

Vous procéderez de la façon suivante :
1er test : Vous lancez un seul téléchargement, et à la fin, vous traitez le fichier .pcap avec votre programme C et vous créez la figure correspondante.
2ème test : Pareil que le premier test, mais vous lancez deux téléchargements en parallèle sur le même serveur. À la fin, vous traitez le fichier .pcap avec votre programme C et vous créez la figure correspondante.
3ème test : Pareil que le test numéro 2, mais avec 3 flux parallèles/
4ème,5ème ... test : Exécutez d'autres tests qui vous semblent intéressants, en fonction de ce que vous avez obtenu précédemment. Vous pouvez, par exemple, passer d'un réseau sans-fil à un réseau Ethernet, cibler différents serveurs pour un même test, etc.

À l'aide des figures obtenues, vous devez écrire un rapport et commenter les résultats. N'oubliez pas de décrire l'environnement de travail en détail (vous étiez dans le campus, sur un réseau sans-fil, etc). Expliquez également pourquoi ces résultats sont différents ou similaires à ce qu'on attendait.
Ce que vous devez rendre

 Le code source de votre programme (qui vous donnera jusqu'à 60% de la note totale, selon la procédure d'évaluation décrite plus tard), un README détaillant tous les aspect nécessaires à connaître pour compiler et exécuter votre programme, plus un Makefile, si nécessaire (10% de la note totale). 

Vous devez fournir également le rapport en format PDF. Compressez tout (rapport + code source + README + Makefile) dans un fichier compressé en format .tgz. Ne fournisez pas les traces .pcap.
Quelques notes à propos de la manipulation des fichiers .pcap

Avant tout, prenez en compte que l'objectif de cette page est de vous décrire ce que vous devez faire dans le projet. En aucun cas vous trouverez ici une description détaillée et suffisante des technologies qui vous seront utiles pour la réalisation du projet. C'est donc de votre responsabilité de mieux vous documenter sur elles.

Afin de manipuler de fichiers .pcap, vous allez utiliser la librairie libpcap. Pour ouvrir un fichier .pcap en mode lecture, libpcap vous fournit la fonction pcap_open_offline().

Pour parcourir un fichier .pcap existant que nous avons précédemment ouvert avec la fonction pcap_open_offline(), nous faisons appelle à la fonction pcap_next(). pcap_next() va donc nous donner chaque paquet capturé, un par un. Une fois ayant obtenu un paquet, le premier en-tête que vous trouverez correspond à l'en-tête de la trame MAC. Sans aller trop loin dans le détails (nous n'avons absolument pas besoin de le faire), tenez bien en compte le fait que l'en-tête MAC est codé sur les premiers 14 octets du paquet, et que les derniers 2 octets (de l'en-tête MAC) correspondent à un champ appelé "Type". Si le type est égal à 0x0800, alors juste après l'en-tête MAC nous avons l'en-tête IP.

Comme toujours, il est très important de fermer les fichiers ouverts. Un fichier ouvert par l'appelle à pcap_open_offline() se ferme par une appelle à la fonction pcap_close().

Prenez également en compte que les librairies à utiliser lors que nous faisons un programme au niveau utilisateur (le "userspace") se trouvent généralement dans le dossier /usr/include/. Dans ce dossier, le répertoire net/ contient des librairies utiles pour la manipulation des en-têtes MAC, et netinet/ des librairies utiles pour la manipulation des protocoles de la famille INET.
Et maintenant, quelques notes sur la méthode d'évaluation

Nous listerons maintenant les étapes qu'interviendront lors de l'évaluation de votre projet. Notez que ces étapes seront évalue dans cet ordre et que si l'une des étapes n'est pas réussie, les points qui resteront ne seront pas pris en compte.
Compilation
Exécution réussi du programme 
Management des erreurs
Rapport
Qualité du code
Point extra : Interface utilisateur
Quelques liens utiles
http://www.tcpdump.org/
http://www.networksorcery.com/enp/default1101.htm
http://www.tcpipguide.com/