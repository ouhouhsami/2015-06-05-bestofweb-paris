# Best Of Web


SG : Développeur Web

NS : Chercheur, Designer son et interaction

---

Un lieu qui réunit des **musiciens**, des **chercheurs**, des **ingénieurs**
dans le but de **renouveller l'expression musicale** contemporaine
à travers la **science** et la **technologie**

---

Audio et Musique, au cœur des problématiques Ircam : 7 équipes de recherche : Acoustique instrumentale, Espaces acoustiques et cognitifs, Perception et design sonores, Analyse & synthèse des sons, Représentations musicales, Analyse des pratiques musicales, Interaction son musique mouvement

Web : dissémination des savoir scientifiques, des base de données de compositeurs, d'œuvres, et, des outils pour la musicologie numérique.
Développement d'outils d'écoute actives (projet Ecoutes signées)
Comment les compositeurs, interprètes ... écoutent.

Et avec Norbert on a décidé de réunir les deux.

Au moment ou le "Web Audio" émergent véritablement pour des applications exigentes

Et est accessible sur (quasi) tous les périphériques connectés de dernière génération

#### Pourquoi transférer des savoirs, des technologies, des algorithmes d'informatique musicale de l'Ircam vers la plateforme Web ?

* 3 000 000 000 d'utilisateurs - s'adresser au plus grand nombre
* *Browser As An OS*, pas d'installation - "TTM" minimal
* Plateforme partagée, multi-utilisateurs, temps réel et multimédia
* Nouveaux champs d'expérimentation et de recherche et retours utilisateurs

ex. Word → Google Doc

---

* 1995 : &amp;lt;blink&amp;gt; midifile et protocoles propriétaires (RTP, RTSP)
* 1997 : côté client avec le plugin et côté serveur avec FMS et octobre 2008 Sound API dans Flash pour faire du traitement audio, minimal
* 2008 : HTML5 &amp;lt;audio&amp;gt;
* 2010 : HTTP streaming (DASH), WebRTC et WebSockets pour l'échange de données, Wep Audio API (première implémentation Chrome 2011). Web Audio API disponible sur Edge

Web Audio !== Web Audio API

20 ans après la première possibilité de lire un son dans le navigateur, les standards proposent un ensemble de fonctionnalités primitives pour créer des séquenceurs audios, des plugin d'effets des synthétiseurs

... et tout ce que l'on peut imaginer comme application musicale dans un environment massivement multimédia, multi-utilisateurs et collaboratif !

Même s'il y a encore des choses qui manquent et à améliorer.

---

Web Audio API 1

---

Synthèse par distorsion non linéaire

* Analyses dans les domaines temporel et fréquenciel *pour la visualisation seulement à l'heure actuelle*

---

AudioContext contient
* le graph du signal audio <small>(connections entre AudioNodes)</small>
* les factory pour créer des AudioNodes <small>(GainNode, PannerNode ...)</small>
* la destination <small>(la sortie audio)</small>
* le currentTime <small>(utile pour ordonnancer les évènements)</small>
* le decodeAudioData

Des AudioNode
* qui vont composer votre graph audio.
* Par exemple l'OscillatorNode qui peut jouer un son sinusoïdal ou encore le GainNode qui permet d'ajuster le volume.

AudioParam
* contrôle un aspect individuel du fonctionnement d'un AudioNode, comme la fréquence d'un oscillateur par exemple
* peut être a-rate <small>valeur pour chaque échantillon d'un block</small> ou k-rate <small>valeur utilisée pour l'ensemble du block</small>
* Méthodes: setValueAtTime(), linearRampToValueAtTime(), exponentialRampToValueAtTime(), setTargetAtTime(), setValueCurveAtTime()
* peut être connecté à un AudioNode: AudioNode.connect(AudioParam) <small>(en plus de AudioNode.connect(AudioNode))</small>, usage type les LFO

---

1. Création de l'audiocontext, qui contiendra notre graph audio
2. Création d'un oscillateur
3. Création de l'enveloppe de volume
4. Création d'un filtre
5. On connect l'oscillateur à l'enveloppe de volume puis l'enveloppe de volume au filtre

On utilise la fonction 'playNote' pour déclencher un son, c'est à dire régler la fréquence de l'oscillateur sur la note que l'on veut jouer et déclencher une enveloppe de volume (durée d'attaque et de release)

---


browserify

grâce au bac à sable de la plateforme web

* AudioWorker : plus de frontière de thread à traverser comme les traitements audio et JavaScript seront sur le même thread
* asm.js, langage intermédiaire constituant un sous-ensemble du langage Javascript, qui ne produit pas d'objet temporaire à passer au ramasse miette.
* SIMD.js SIMD (Single Instruction Multiple Data) qui permet de faire des opérations sur des éléments multiples ensemble, et qui a des répercutions interessantes en terme de performance sur le traitement de buffer audio.

* Pour les mauvaises nouvelles (denormals, lock-free/wait-free, context-switch), [regardez la vidéo](http://medias.ircam.fr/x2af2f6).

=> Avec ces optimisation, le code Web Audio Api est 50% plus long que du code natif.

---


Aborde les questions que la Web Audio API et d'autres standards ne résolvent pas (il ne s'agit pas d'un wrapper d'API).

---


Avec HTML5, de nouvelles API et de nouveau type d'input (color, range, number)

Mais rien pour pour waveform et les timeline.

Modulaire, commandé par les données, SVG

---

ex. Web Audio API : l'ordonnancement des évènements pour des applications
 audio interactives (notamment la lecture audio) peut être très complexe à gérer.

Moteurs : créent un buffer et le jouent

1. Granular
2. Segment
3. Transport

---
