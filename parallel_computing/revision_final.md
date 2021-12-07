1. Avec OpenCL, est-ce que la copie d’un buffer RAM vers un buffer le dispositif implique la « Command Queue »?  
  - Oui, quand on send/receive des donner du device vers le host, on utilise le a Command Queue

2. Un « Program » OpenCL peut-il contenir plusieurs Kernels? Plusieurs Contextes? 
  - Oui, puisqu'on peut avoir un context CPU et un context GPU

3. Avec CUDA, la mémoire partagée est accessible par quoi? Avec OpenCL, la mémoire locale 
est accessible par quoi?
  - CUDA : bloc de threads GPU
  - OpenCL: Memoire locale OpenCL = memoire partagée CUDA

4. Avec CUDA, une fonction utilitaire peut-elle être compilée pour CUDA et pour le CPU en 
même temps? Comment? 
  - Oui, on peut mettre __device__ et __host__ comme modificateur a la fonction. Par default,
  une fonction a le modificateur __host__
  - Global : declare que la fonction est un kernel

5. Quel est l’équivalent du ID d’une tâche pour OpenCL? Est-ce aussi possible de l’obtenir en 
plusieurs dimensions? Si oui, comment? 
  - Oui, avec getGlobalId 0 = x, 1 = y, 2 = z, pas besoin de passer par la danse de calcul
  necessaire en CUDA pour obtenir le id du thread

6. Considérons l'addition de matrices où chaque élément de la matrice de sortie est la somme 
des éléments correspondants des deux matrices d'entrée. Peut-on utiliser la mémoire partagée 
pour améliorer la performance du Kernel ? Justifiez. 
  - Non, simple lecture et pas de dependance 

7. En supposant que la capacité n'est pas un problème pour les registres (on a une quantité 
infinie) et que le temps d’accès à un registre est de 1 cycle d’horloge comparé à 5 cycles 
d’horloge de la mémoire partagée/cache, donnez un cas où il serait intéressant d'utiliser la 
mémoire partagée au lieu des registres pour conserver les valeurs extraites de la mémoire 
globale. Expliquez votre réponse.
  - Registre : Prive a chaque thread, donc si tous les threads doit copier de la memoire globale
    vers ses registres, alors on a plus d'acces en memoire globale que si on copiait de la memoire
    globale vers la memoire partagee

8. Imaginez que vous devez écrire un filtre de convolution 2D pour traiter une image de taille 76x62.
  a) 5 x 4
  b) 3 x 2
  c) 
    - a -> (76 * 32) - (16 * 16 * 20) 
    - b -> (76 * 32) - (32 * 32 * 6)

9. Si le SM d'un dispositif CUDA peut prendre jusqu'à 1536 threads et jusqu'à 4 threads blocs. 
Parmi les configurations de blocs suivantes, laquelle entraînerait le plus grand nombre de 
threads dans le SM ? le plus grand nombre de threads dans le SM ?
  - C), parce qu'on pourrait avoir 3 threads par bloc et avoir un occupancy de 100%. 3 * 512 = 1536

10. A) Dans le dernier bloc, le  
    C) 256 - 7

11. Dans une implémentation OpenCL, avons-nous besoin d'une barrière synchronisation avant 
l'exécution du kernel pour garantir que les données ont été transférées de l'hôte vers le 
dispositif ? Justifiez votre réponse.
  - Non, parce qu'on a une command queue

12. Dans une implémentation OpenCL, avons-nous besoin d'une synchronisation après 
l'exécution du kernel pour garantir que les données ont été copiées du périphérique vers l'hôte 
avant d'utiliser les résultats dans l'hôte ? Justifiez votre réponse.

12b. Cuda on a pas besoin si on utilise un cudeMallocManage. 

13. Vous devez écrire un kernel qui opère sur une image de taille 400 × 900 pixels. Vous 
souhaitez affecter un thread à chaque pixel. Vous souhaitez que vos blocs de threads blocs de 
threads soient carrés et que vous utilisiez le nombre maximum de threads par bloc possible 
sur le périphérique (votre périphérique a une capacité de calcul 7.5). Comment allez-vous 
sélectionnez-vous les dimensions de la grille et des blocs de votre kernel ?
  - bloc: 20 x 20

15. Comment doit-on configurer la grille de travail afin d'exécuter un noyau OpenCL ? Quelles 
sont les principales variables impliquées ? Existe-t-il une relation entre ces variables ?
  - Global dimension : taille de notre probleme selon la taille de notre probleme
    - 400 * 900 
  - Local dimension : taille de notre workgroup -> equivalent de notre work group dans CUDA 
    - ici 16 x 16 = 256
    - OpenCL calcul apres le nombre de bloc a allumer
  - *Global dimension doit etre parfaitement divisible par la local dimension*

17. Operations dependante write et read, alors on doit sync les threads pour eviter d'avoir
    une race condition

18. Vrai ou Faux : La taille d’un carreau dans l’algorithme de multiplication de matrice par 
carreaux est limitée par la taille d’un bloc de thread. 
  - Faux, un thread peut traiter plus qu'une valeure

21. Pour la multiplication de matrice (C = A * B) avec l’algorithme des carreaux (tiling) basée 
sur une disposition rangée-major, quelle matrice d'entrée aura des accès à la mémoire globale 
coalescés ? Est-ce que ça change avec l’implémentation simple (sans utilisation des carreaux 
et de la mémoire partagée)?
  - acces mémoire globale coalescés: acces consecutif
