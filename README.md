# check_dois_in_hal
<h1>Vérification de la présence de DOIs dans Hal, par lot</h1>
<h2>En un mot</h2>
L’outil est construit sur l'API Hal. Son objectif est de pointer, parmi un <b>lot</b> de DOIs, ceux  qui sont <b>absents</b> de Hal. 
<br/>
L’utilisateur est invité à uploader un fichier .csv contenant une colonne de DOIs
<br/>
Dès que le choix du fichier est fait, le processus s’enclenche. A la fin du processus, l’utilisateur peut décharger les DOIs manquants dans Hal sous la forme d’un fichier .csv
<h2>Langage</h2>
JavaScript<br/>
N'importe quel browser permet d'utiliser le code
<h2>Fichiers</h2>
Pour permettre une instalation la plus facile possible tout le code (toutes les fonctions) se trouve dans un seul fichier, upload_dois_and_check_against_hal.html
<br/>
Dans le répertoire test se trouve un fichier nommé 40_DOIs.csv contenant une colonne de DOIs. Il permet de tester l'outil
<h2>Dépendance</h2>
L'outil est dépendant de l'API Hal telle qu'elle existe aujourd'hui (décembre 2024) avec le point d'entrée https://api.archives-ouvertes.fr/search<br/>
La documentation de l'API Hal : <a href='https://api.archives-ouvertes.fr/docs/search' target='_blank'>https://api.archives-ouvertes.fr/docs/search</a>
<h2>fonctionnalités, fonction</h2>
La fonction upload_files_function() sert à uploader le fichier<br/>
A l'intérieur de cette fonction, la fonction csv_to_array_function() sert à nettoyer les données entrantes afin qu'à la fin de chaque ligne il y ait un \r et rien d'autre<br/>
La fonction download_file_function() sert à downloader le fichier de résultat<br/>
A l'intériure de cette fonction, la fonction array_to_csv_function() transforme l'array dans laquelle ont été stockés les résultats (dois_missing_in_hal) en une chaîne de caractère qui sera comprise comme un .csv à une seule colonne : des données séparées par un \n\r, ie une passage à la ligne<br/>
La fonction get_hal_data_function() prend une array de DOIs entrée, les passe en revue via un while et, chaque fois, interroge l'API Hal à la recherche de la donnée "response" >>> "numFound". Si cette donnée est à zéro, cela signifie que le DOI n'est pas dans Hal, et donc mérite d'êtres stocké (dans l'array dois_missing_in_hal). A noter, le while mis en oeuvre ici est ralenti par la commande await new Promise(r => setTimeout(r, 10));
