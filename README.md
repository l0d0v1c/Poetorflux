# Poetor

Générateur de poésie française par réseau de neurones récurrent (2018).

Projet antérieur à l'essor des Transformers. Là où les LLM modernes (GPT, Claude, LLaMA) utilisent des architectures Transformer avec des milliards de paramètres et tokenisent le texte en sous-mots, Poetor prend le chemin inverse : un petit LSTM de **3 millions de paramètres** qui génère de la poésie **caractère par caractère**.

## Architecture

```
Entrée (one-hot, 37 caractères)
        │
   LSTM 500 unités
        │
   LSTM 500 unités
        │
   Dense 37 + softmax
        │
Sortie (caractère suivant)
```

- **Vocabulaire** : 37 caractères — les 26 lettres minuscules, 10 lettres accentuées (é è ê î ï ô œ à â ù) et l'espace
- **Entraînement** : corpus de poésie française (19e et 20e siècles), caractère par caractère, optimiseur RMSprop
- **Poids** : 3 096 537 paramètres, 12 Mo en float32

Le modèle n'a aucune notion de mot, de grammaire ou de syntaxe. Il apprend les régularités statistiques du français poétique à l'échelle du caractère : enchaînements de lettres, structures syllabiques, rythmes. Les mots et les vers émergent d'eux-mêmes.

## Démos

### 



### `poetorflux.html` — Flux continu

Génération ininterrompue de poésie en temps réel. Le texte s'écoule caractère par caractère, ligne après ligne.

## Exemple de sortie

```
Bre et les crasseurs rend plus rien
Ne s'asseyait sur les coeurs lointains et
Des troncs moussus aux cris des soirs
De ses yeux son histoire ouverte aux
Lueurs furent sans effort son nid d'air
Naboe qui pourrait disparaît le cou non
Pas un baiser de l'autel un peuple
De fleurs qui n'a bayant souffert
L'homme est un ciel d'azur à wallirère
Ô soleils ii celui des amis et
Les dieux du nord qui te réclame
```

## Contexte

En 2018, les réseaux récurrents (LSTM, GRU) étaient l'approche dominante pour la génération de texte. "Attention Is All You Need" venait d'être publié (2017) et les premiers GPT n'existaient pas encore en tant que produits. Ce projet illustre ce qu'un modèle minimal, entraîné sur un corpus spécialisé, peut produire : des textes qui ressemblent à de la poésie sans jamais avoir appris ce qu'est un mot.
