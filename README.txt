R�seaux et Internet
 Performance TCP 
Description du Projet

Dans ce projet vous devez �tudier la performance d'un �metteur TCP du point de vue du d�bit.

Pour commencer, vous devez donc estimer le d�bit des connexions TCP, � l'aide d'un programme C qui :
lira un fichier .pcap contenant des paquets captur�s avec le logiciel Tcpdump ou Wireshark
v�rifiera la pr�sence de paquets TCP
Pour chaque flux TCP produira un fichier texte th-flowid.txt (o� flowid correspond � l'identifiant TCP du flux en question), qui contiendra 2 colonnes : une colonne temps, une colonne d�bit

Le d�bit sera calcul� sur des intervalles r�gulier d'une seconde et le d�bit correspondant � chaque intervalle de temps sera donn� en Kilobits par second (Kbps). Notez que le d�bit TCP sera calcul� uniquement en fonction de la charge utile de chaque paquet. Enfin, � l'aide de n'importe quel outil, vous produirez une image � partir du fichier texte, qui montrera graphiquement l'�volution du d�bit.

Une fois ayant cr�� votre programme C, vous pouvez proc�der � la campagne de test dans laquelle, vous devez t�l�charger des donn�e depuis le serveur de votre choix (en veillant � ce que le temps de t�l�chargement d�passe au moins la vingtaine de secondes), tandis que le trafique r�seau est enregistr� par tcpdump.

Vous proc�derez de la fa�on suivante :
1er test : Vous lancez un seul t�l�chargement, et � la fin, vous traitez le fichier .pcap avec votre programme C et vous cr�ez la figure correspondante.
2�me test : Pareil que le premier test, mais vous lancez deux t�l�chargements en parall�le sur le m�me serveur. � la fin, vous traitez le fichier .pcap avec votre programme C et vous cr�ez la figure correspondante.
3�me test : Pareil que le test num�ro 2, mais avec 3 flux parall�les/
4�me,5�me ... test : Ex�cutez d'autres tests qui vous semblent int�ressants, en fonction de ce que vous avez obtenu pr�c�demment. Vous pouvez, par exemple, passer d'un r�seau sans-fil � un r�seau Ethernet, cibler diff�rents serveurs pour un m�me test, etc.

� l'aide des figures obtenues, vous devez �crire un rapport et commenter les r�sultats. N'oubliez pas de d�crire l'environnement de travail en d�tail (vous �tiez dans le campus, sur un r�seau sans-fil, etc). Expliquez �galement pourquoi ces r�sultats sont diff�rents ou similaires � ce qu'on attendait.
Ce que vous devez rendre

 Le code source de votre programme (qui vous donnera jusqu'� 60% de la note totale, selon la proc�dure d'�valuation d�crite plus tard), un README d�taillant tous les aspect n�cessaires � conna�tre pour compiler et ex�cuter votre programme, plus un Makefile, si n�cessaire (10% de la note totale). 

Vous devez fournir �galement le rapport en format PDF. Compressez tout (rapport + code source + README + Makefile) dans un fichier compress� en format .tgz. Ne fournisez pas les traces .pcap.
Quelques notes � propos de la manipulation des fichiers .pcap

Avant tout, prenez en compte que l'objectif de cette page est de vous d�crire ce que vous devez faire dans le projet. En aucun cas vous trouverez ici une description d�taill�e et suffisante des technologies qui vous seront utiles pour la r�alisation du projet. C'est donc de votre responsabilit� de mieux vous documenter sur elles.

Afin de manipuler de fichiers .pcap, vous allez utiliser la librairie libpcap. Pour ouvrir un fichier .pcap en mode lecture, libpcap vous fournit la fonction pcap_open_offline().

Pour parcourir un fichier .pcap existant que nous avons pr�c�demment ouvert avec la fonction pcap_open_offline(), nous faisons appelle � la fonction pcap_next(). pcap_next() va donc nous donner chaque paquet captur�, un par un. Une fois ayant obtenu un paquet, le premier en-t�te que vous trouverez correspond � l'en-t�te de la trame MAC. Sans aller trop loin dans le d�tails (nous n'avons absolument pas besoin de le faire), tenez bien en compte le fait que l'en-t�te MAC est cod� sur les premiers 14 octets du paquet, et que les derniers 2 octets (de l'en-t�te MAC) correspondent � un champ appel� "Type". Si le type est �gal � 0x0800, alors juste apr�s l'en-t�te MAC nous avons l'en-t�te IP.

Comme toujours, il est tr�s important de fermer les fichiers ouverts. Un fichier ouvert par l'appelle � pcap_open_offline() se ferme par une appelle � la fonction pcap_close().

Prenez �galement en compte que les librairies � utiliser lors que nous faisons un programme au niveau utilisateur (le "userspace") se trouvent g�n�ralement dans le dossier /usr/include/. Dans ce dossier, le r�pertoire net/ contient des librairies utiles pour la manipulation des en-t�tes MAC, et netinet/ des librairies utiles pour la manipulation des protocoles de la famille INET.
Et maintenant, quelques notes sur la m�thode d'�valuation

Nous listerons maintenant les �tapes qu'interviendront lors de l'�valuation de votre projet. Notez que ces �tapes seront �value dans cet ordre et que si l'une des �tapes n'est pas r�ussie, les points qui resteront ne seront pas pris en compte.
Compilation
Ex�cution r�ussi du programme 
Management des erreurs
Rapport
Qualit� du code
Point extra : Interface utilisateur
Quelques liens utiles
http://www.tcpdump.org/
http://www.networksorcery.com/enp/default1101.htm
http://www.tcpipguide.com/