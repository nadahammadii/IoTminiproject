#Les Composants utilisé:

#1 la carte STM32L475VGT6:
![image](https://github.com/nadahammadii/IoTminiproject/assets/148150733/bfbc5afb-f842-43ce-b394-54f8df42d92c)

#2 Smartphone connecté a l’internet:
Le smartphone agit comme client, interagissant avec le serveur HTTP int´egr´e sur la carte
B L475E-IOT01ax via le module Es-WiFi. Les utilisateurs acc`edent au serveur via le
navigateur de leur smartphone, permettant la manipulation des LED et la surveillance des
capteurs de temp´erature, avec des informations en temps r´eel affich´ees sur le smartphone
via Hyperterminal


#.3 source d’internet:
une source d’internet comme un modem pour connect´e le module wifi de la carte avec le
l’internet.

#4 description detaillée:
Ce projet pr´esente la mise en œuvre de requetes HTTP a l’aide du module Es-WiFi
bas´e sur STM32Cube HAL. En utilisant le module Es WiFi et un navigateur web,
l’application d´emontre la cr´eation d’un serveur web simple sur la carte B L475E-IOT01ax. En accédant a l’adresse IP du bouclier es-WiFi via un navigateur,
la carte r´epond aux requˆetes HTTP de maniere transparente.
Le projet offre un exemple concret de communication entre un client HTTP et un
serveur, ou le bouclier Es-WiFi sur la carte B L475E-IOT01ax agit en tant que serveur.
L’application prend en charge l’interaction avec un smartphone, avec des instructions
d´etaill´ees disponibles dans la section ”Environnement mat´eriel et logiciel”.
Pour am´eliorer l’exp´erience utilisateur, les messages de journalisation sont affich´es sur
Hyperterminal via USART, fournissant des informations en temps r´eel sur l’´etat du
module es wifi lorsque #define TERMINAL USE est activ´e dans main.c. La
communication s’effectue via une application de navigateur web sur un smartphone.
Le serveur HTTP int´egr´e dans le projet comprend une page HTML avec deux
fonctionnalit´es principales :
1- Contrˆole des LED :
permet aux utilisateurs de manipuler la LED verte (LED2) sur la carte
B L475E-IOT01ax.
2- Conversion ADC :
affiche la valeur convertie du capteur de temp´erature, offrant des informations sur la
temp´erature ambiante.
#5 Implementation de projet
#6 ´etape 1:
Creation d’un nouveau projet dans stm32cubeIde software
![image](https://github.com/nadahammadii/IoTminiproject/assets/148150733/72912c7c-0c83-46dc-8eef-1e875651f810)
#.7 ´etape 2:
selectionner la carte en ecrivant le nom de famille de la carte ensuite appuit sur le button
next au dessous de fenetre
![image](https://github.com/nadahammadii/IoTminiproject/assets/148150733/a3fa6107-8cc3-459b-95ac-c6893c495151)
#.8 ´etape 3:
enfin le projet est cr´ee maintenant il faut selectionner le pin PB14(green Led) en output

![image](https://github.com/nadahammadii/IoTminiproject/assets/148150733/8b3bef26-a4fd-4480-a8ab-65604679d2f7)
#9 ´etape 4:
maintenant en va selectionner le protocole UART .il faut selectionner un l’un pour j’ai
selectionner UART4 ensuite il modifier le mode comme asynchrone et `a la fin il faut
generer le code en appuiyant sur le button Tool code generation au dessus de fenetre


![image](https://github.com/nadahammadii/IoTminiproject/assets/148150733/cca59be1-c495-4b74-a333-c87242fa8987)



![image](https://github.com/nadahammadii/IoTminiproject/assets/148150733/72bae7f0-4565-4694-96fb-ee92d3958228)
#.10 ´etape 5:
Pour utilisez le module wifi interne de la carte il faut ajouter ces 3 fichier es wifi.c,
es wifi io.c , wifi.c et wifi.h. pour cela en va cr´eer un fichier nomm´ee et on va ajouter
dans le les 3 fichier es wifi.c, es wifi io.c , wifi.c .par le fichier wifi.h en va cr´eer un fichier
dans core\Inc.en va ajouter pour chaque fichier leur code.


![image](https://github.com/nadahammadii/IoTminiproject/assets/148150733/98b08c86-f751-41f1-93e5-ef2de70bbbe1)


#.11 ´etape 6:
Pour utilisez le capteur de temperateur interne de la carte il faut ajouter ces 2 fichier
stm32l475e iot01 tsensor.c et stm32l475e iot01 tsensor.h. pour cela en va cr´eer un fichier
dans Drivers\stm32L4xx HAL Driver nomm´ee stm32l475e iot01 tsensor.c. ensuite on va
cr´eer un fichier nomm´ee stm32l475 iot01 tsensor.h core\Inc.en va ajouter pour chaque
fichier leur code

![image](https://github.com/nadahammadii/IoTminiproject/assets/148150733/d83725ec-dfe0-4e58-8458-4615e9ea5e60)
#12 ´etape 7: Ajout d’une partie code dans le fichier main.c
la fonction wifi start initialise le module ESWIFI en appelant la fonction WIFI Init(). Si
l’initialisation est r´eussie,
elle affiche un message de journalisation indiquant que le module ES-WIFI a ´et´e initialis´e
avec succ`es.
Ensuite, elle r´ecupere l’adresse MAC du module en appelant la fonction WIFI GetMAC Address().
Si la r´ecup´eration de l’adresse MAC est r´eussie, elle affiche l’adresse MAC dans le format
: En cas d’´echec de l’initialisation ou de la r´ecup´eration de l’adresse MAC, elle affiche un
message d’erreur et retourne -1.

![image](https://github.com/nadahammadii/IoTminiproject/assets/148150733/b214a00f-629e-400e-99cf-72bc52d56469)
la fonction wifi connect commence par appeler la fonction wifi start() pour initialiser le
module WiFi et r´ecup´erer son adresse MAC. Ensuite, elle affiche un message de
journalisation indiquant la tentative de connexion avec les informations SSID et
PASSWORD en utilisant le protocole UART. Si la connexion WiFi est ´etablie avec
succ`es en appelant WIFI Connect(), elle recupere l’adresse IP attribu´ee au module avec
WIFI GetIP Address(). Si la r´ecup´eration de l’adresse IP est r´eussie, elle affiche
l’adresse IP dans le format : En cas d’´echec de la connexion Wi-Fi ou de la r´ecup´eration
de l’adresse IP, elle affiche un message d’erreur correspondant et retourne -1.



![image](https://github.com/nadahammadii/IoTminiproject/assets/148150733/efc5482a-dc5c-42c4-8d30-497705c90158)
le fonction SendWebPage construit une page web dynamique avec des informations
sp´ecifiques telles que la temp´erature ambiante et l’´etat de la LED, puis l’envoie au client via le module WiFi. La page g´en´er´ee contient un formulaire permettant de
visualiser et de modifier la temp´erature ainsi que de contrˆoler l’´etat de la LED. La
fonction utilise des fonctions de manipulation de chaˆınes pour construire le contenu
HTML, et envoie ensuite ces donn´ees via WIFI SendData()

![image](https://github.com/nadahammadii/IoTminiproject/assets/148150733/c701218b-3814-413f-a672-4d24418d6e51)

la fonction WebServerProcess lit les donn´ees entrantes du client via le module WiFi en
utilisant WIFI ReceiveData(). Elle v´erifie si la requˆete contient la chaˆıne ”GET” ou
”POST” et effectue des actions sp´ecifiques en fonction de la requˆete. Si la requˆete est
de type GET, elle r´ecupere la temp´erature a l’aide du capteur de temp´erature et envoie
une page web dynamique avec ces informations en appelant la fonction SendWebPage().
Si la requˆete est de type POST, elle analyse le contenu de la requˆete pour effectuer des
actions sp´ecifiques, telles que la mise a jour de l’´etat de la LED oul’arrˆet du serveur en
fonction des param`etres de la requˆete.


![image](https://github.com/nadahammadii/IoTminiproject/assets/148150733/5af39a79-6a7d-4e8f-8147-acda22c47203)


![image](https://github.com/nadahammadii/IoTminiproject/assets/148150733/62416e34-a629-459e-afee-5c7be1c288cc)
la fonction wifi server lit les donn´ees entrantes du client via le module WiFi en utilisant
WIFI ReceiveData(). Elle v´erifie si la requˆete contient la chaˆıne ”GET” ou ”POST” et
effectue des actions sp´ecifiques en fonction de la requˆete. Si la requˆete est de type GET,
elle r´ecupere la temp´erature a l’aide du capteur de temp´erature et envoie une page web
dynamique avec ces informations en appelant la fonction SendWebPage(). Si la requˆete
est de type POST, elle analyse le contenu de la requˆete pour effectuer des actions
sp´ecifiques, telles que la mise a jour de l’´etat de la LED oul’arrˆet du serveur en fonction
des param`etres de la requˆete

![image](https://github.com/nadahammadii/IoTminiproject/assets/148150733/20daf98f-cc30-4177-8cc9-06d297c90374)
on va ajouter cette partie de code pour initialiser le ssid et le password de wifi


![image](https://github.com/nadahammadii/IoTminiproject/assets/148150733/c3c99ebe-e41a-41a8-aba0-14c28bdd5a63)
on va appell´e la fonction dans wifi server le boucle while

![image](https://github.com/nadahammadii/IoTminiproject/assets/148150733/14892826-0549-406f-8a1f-da0fb428b9a6)

#13 ´etape 8:
pour faire l’execution il faut implement´e la carte avec le pc en utilisant le cable usb.
ensuite en va cliqu´e sur le button d’execution au dessus de fenetre .si l’execution termine
sans erreur on va saisir l’adresse ip de carte sur l’internet avec le smartphne pour obtenir
notre page web

![image](https://github.com/nadahammadii/IoTminiproject/assets/148150733/0d53496c-6684-49aa-ad70-18652e4008f2)
Resultat de l’execution :

![image](https://github.com/nadahammadii/IoTminiproject/assets/148150733/aed3d881-9f9c-4b86-85c4-3ed5251ef8e9)

