# REVISION GTI780

## Exercice 3
1. 

P1: drones.01.altitude : A, C
P2: drones.02.latitude : B, C, D
P3: drones.01.latitude : B, C

2.
State: A: S1, B: S2, C: S3, D: S5
P1: A: S1, C: S3

State: A: S2, B: S2, C: S4, D: S5
P2:B: S2, C: S4, D: S5

State: A: S2, B: S3, C: S5, D: S6
P3: B: S3, C: S5

---------------------------------------

State: A: S2, B: S3, C: S3, D: S6
P1: A: S2, C: S3

State: A: S1, B: S2, C: S4, D: S6
P2:B: S2, C: S4, D: S6

State: A: S1, B: S3, C: S5, D: S5
P3: B: S3, C: S5

--------------------------------------

State: A: S1, B: S2, C: S3, D: S5 -> On revient a notre state inital

S1: 1, S2: 3, S3: 4, S4: 2, S5: 3, S6: 1 * 5

S1: 5, S2: 15, S3: 20, S4: 10, S5: 15, S6: 5

## Conferencier

Key Security Threats : Modele OWASP
9. Pas la protection physique necessaire

8. Insecure default settings
- Mot de passe par default pas assez securitaire (admin, admin)

7. Insecure data transfer and storage
- Manque d'encryption au niveau des donnes soit en transit ou at rest
  - Pas de HTTPS/TTS et pas d'encryption des donnees sur le disk

6. Insufficient Privacy Protection
- Stockage de la vie prive sur le device

5. Use of Insecure and outdated components
- Utilisation de 3rd party package vulnerable

4. Lack of secure Update Mechanism
- Comment s'assurer que l'on livre un firmware update qui ne sera pas 
  hijacked (man in the middle)
- Encrypt le firmeware update ? Device p-e pas assez puissant pour decrypt
- Software et AI industriel : Perdu model
    0 - Process level : mesure se fait (device qui recolte data)
    .
    .
    .
    5 - Entreprise Network : Bureau dans lequel y'a un ordi et user dessus
    O - 3 : OT (Operation Technologie) 4 - 5 IT Level
    Firewall entre 4 et 3 pour proteger les devices de l'exterieur, donc 
    difficile de faire faire un firmeware update

3. Insecure Ecosystem Interfaces
- Back end and frontend qui serait pas securitaire

2. Insecure Network Services
- Port qui reste ouvert pour rien qui rend vulnerable nos appl

1. Weak, Guessable or hardcoded password
- Code pourrait contenir des informations sensibles comme des password 
qui pourrait etre commit sur un repo

### State of Security
- Les updates apporter sur un device rend les devices encore plus vulnerable 
