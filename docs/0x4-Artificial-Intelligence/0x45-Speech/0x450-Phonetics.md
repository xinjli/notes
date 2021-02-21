# 0x450 Phonetics

## Foundation
- phoneme: abstract sound unit distinguishing one word from another in a particular language (e.g.: /t/)
- phone: actual sound produced in speech (independent of languages) (e.g: [t])
- allophone: a set of phones to represent a phoneme in a particular language (phoneme/allophone is something like class/instance)
Substituting one phoneme for another will result in a word with a different meaning, but substituting allophones only results in a different pronunciation of the same word.

### Speaking System
Airflow: 

- Powering up lungs
- Buzzing with the vocal folds in the larynx
- Shaping the airflow


## Articulatory Phonetics
- voiced: sounds produced when vocal folds are vibrating
- voiceless: sounds produced when vocal folds are apart
  
#### Articulators
- movable articulators: Tongue, Jaw, Lips, velum (soft palate)
- static articulators: Teeth, Alveolar ridge, Hard palate

#### airstream mechanism

direction
- egressive: inside to outside
- ingressive: outside to inside
- 
place
- pulmonic: lung
- glottalic: glottal
- velaric: velar
- 
### Consonants
A consonant is a sound made by partially or totally blocking the vocal tract during speech production. 

Consonants are classified based on where they are made in the articulatory system (place of articulation), how they are produced (manner of articulation), whether they are voiced or not.

Stop consonants
aspiration: a period after the release of the lip closure (e.g: "pie", "tie", "kie"). In xsampa, it is marked as _h suffix

#### place of articulation
the location inside the mouth at which the constriction of air take place

- coronal: speech sounds made using tip or blade

- dorsal: speech sounds make using the rear of the tongue

- bilabial: sounds made with a constriction at the lips (e.g: pat, bat)

- labiodental: top teeth touch bottom lip (e.g: fat, vat)

- dental: a closure produced at the teeth with contact of the tongue tip and/or blade (e.g: this, thick)

- alveolar: ridge on hard palate (e.g: t, d, s, z)

- retroflex: tongue tip to the rear of the alveolar ridge, common in India, Pakistan English, rare in American British English

- palato-alveolar (post alveolar):  place tongue blade behind alveolar ridge (e.g: ship)

- palatal: tongue on the hard plate (e.g: yes, yellow)

- velar: tongue on the soft palate

### Vowels
- [i] has low F1 and high F2
- [a] has high F1 and low F2
- [u] has low F1 and low F2
  

## Acoustic Phonetics
Formants Rules
- F1 rule(high/low): F1 is inversely related to tongue height, or equivalently related to distance between tongue and palate. For example, the average adults males /i/  (top high vowel) ~300 Hz, /a/ (back low vowel) ~ 754 Hz.
- F2 rule(front/back): more front the tongue is placed, the higher the F2 frequency value.
- F3 rule(retroflexion): everytime an r-colored sound is made, F3 decreases in value
- F1-F3 lowering rule: Lip protrusion will make vocal tract a bit longer (17+2.5cm for male or 14+2.5 cm for female), which makes the resonant peaks go slightly lower. (probably because of the larger $L$ in the following string vibrating formula)

$$f = \frac{nv}{2L}$$

## Reference
[1] Ladefoged, Peter, and Keith Johnson. A course in phonetics. Nelson Education, 2014.

[2] Katz, William F. Phonetics for dummies. John Wiley & Sons, 2013.

