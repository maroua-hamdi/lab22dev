#  LAB 22 — Android JNI (Java ↔ C++)

##  Objectif

Ce TP a pour objectif d'intégrer du code natif C++ dans une application Android en utilisant JNI (Java Native Interface).

L’application permet d’appeler des fonctions C++ depuis Java et d’afficher les résultats dans une interface Android.

---

##  Technologies utilisées

- Java (Android)
- C++ (NDK)
- JNI
- CMake
- Android Studio

---

##  Architecture du projet

```
app/
└── src/
    └── main/
        ├── java/com/example/lab22mobile/MainActivity.java
        ├── cpp/
        │   ├── lab22mobile.cpp
        │   └── CMakeLists.txt
        └── res/layout/activity_main.xml
```
        
---

##  Fonctionnalités implémentées

- Appel JNI depuis Java vers C++
- Calcul du factoriel
- Inversion de chaîne
- Somme d’un tableau
- Gestion des erreurs (valeurs négatives, overflow)
- Logs natifs avec Logcat

---

##  Résultat de l'application

![WhatsApp Image 2026-03-24 at 20 48 23](https://github.com/user-attachments/assets/1f19a8c2-a636-4624-a3f9-5c423f71a5e3)


---

##  Étape 1 → 8 : Mise en place

- Création du projet Android avec support C++
- Configuration Gradle + NDK
- Création du fichier `CMakeLists.txt`
- Implémentation du code C++
- Déclaration des méthodes natives en Java
- Création du layout XML
- Compilation et exécution

---

##  Étape 9 — Logs JNI

Les logs natifs sont affichés dans Logcat avec le tag :JNI_DEMO

### Exemple :

- Appel de helloFromJNI depuis le natif
- Factoriel de 10 calculé = 3628800
- String inversée = !lufrewop si INJ
- Somme du tableau = 150

 Capture :

![WhatsApp Image 2026-03-24 at 21 25 21](https://github.com/user-attachments/assets/f563aff9-de03-4899-a793-8e03cec7d5d2)


---

##  Étape 10 — Tests guidés

### Résultats obtenus :

| Test | Entrée | Résultat |
|------|--------|----------|
| Normal | factorial(10) | 3628800 |
| Négatif | factorial(-5) | -1 |
| Overflow | factorial(20) | -2 |
| String vide | "" | "" |
| Tableau vide | [] | 0 |

📸 Logs Java :

![WhatsApp Image 2026-03-24 at 21 34 16](https://github.com/user-attachments/assets/a8765d8c-378f-4a38-9293-f1c370d081b7)


---

##  Étape 11 — Debug des erreurs

### ❌ UnsatisfiedLinkError
- Mauvais nom de bibliothèque
- Signature JNI incorrecte

### ❌ Erreurs C++
- includes manquants (`<algorithm>`, `<climits>`)

### ❌ Problème String JNI
- oubli de `ReleaseStringUTFChars`

---

##  Étape 12 — Pourquoi JNI ?

JNI est utile pour :

- Calcul intensif
- Réutilisation de bibliothèques C++
- Accès bas niveau
- Optimisation des performances

---

##  Étape 13 — Bonnes pratiques

- Minimiser les appels JNI
- Libérer les ressources (Release...)
- Utiliser Logcat intelligemment
- Garder une API propre

---

##  Étape 14 — Extension (optionnelle)

Exemples possibles :

- Multiplication matricielle
- Détection de caractères interdits
- Benchmark Java vs C++

---

##  Étape 15 — Gestion des exceptions

Possibilité de lever des exceptions Java depuis C++ :

```cpp
env->ThrowNew(env->FindClass("java/lang/IllegalArgumentException"), "Erreur");

##  Conclusion

Ce projet a permis de mettre en pratique l’intégration de code natif C++ dans une application Android à l’aide de JNI.

Il met en évidence :
- la communication entre Java et C++,
- l’utilisation du NDK pour des traitements intensifs,
- ainsi que l’importance de la gestion mémoire et du debugging natif.

Bien que JNI apporte un gain de performance et de flexibilité, son utilisation doit rester maîtrisée en raison de sa complexité.
