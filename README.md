# GATE X-E

Gate X-E is a collection of challenge sets for translation gender rewriters from weakly-gendered languages into English. The set of source languages includes Turkish, Persian, Hungarian and Finnish. Gendered pronouns are not used in any of these languages, so when translating a sentence using third-person pronouns into English, an arbitrary gender will often be assigned in the translation. Gender markings are possible in all of these languages through gendered nouns, however (such as annem - mother in Turkish).

You can find our paper detailing the development of and uses for GATE X-E at https://arxiv.org/pdf/2402.14277.pdf


## Arbitrarily Gender-Marked Entities (AGMEs)
An AGME is a group or individual whose gender is not specified in the a source language, but is given an arbitrary gender marking in the translation. 

In the following example *sister/brother/sibling* is an AGME because it is not specified for gender in the source, but is in the translations. *Father*, however, is marked as male in the source, and so it is not an AGME.

**Source**: *Kardeş*im **babas**ının yemeğini usulca hazırladı.

**Feminine**: My *sister* carefully prepared *her* **father**'s dinner.

**Masculine**: My *brother* carefully prepared *his* **father**'s dinner.

**Neutral**: My *sibling* carefully prepared *their* **father**'s dinner.



## GATE X-E Structure


The data set for each source language consists of between 1250 and 1850 test instances. Each test instance contains the following:
- A sentence in the source language referring to at least one human individual who is marked for gender in the translations
- A set of labels indicating features about individuals mentioned in the translation.
- One or more English translations of the source sentence, covering possible variants with different gender markings. 
    - If there are any AGMEs, it will contain translations where all AGMEs are marked as female, and another where they are all marked as male.
    - If there are two AGMEs, a *variants* column will contain translations with mixed gender markings (i.e. a combination of feminine, masculine and neutral forms) 
	-  If neutral forms for all gendered words exist in common usage, we also include a “neutral” translation. Gendered pronouns use forms of singular *they*. We also include a “full neutral” form, where pronouns referring to non-AGME individuals also use singular *they* forms.
	
Note that any non-AGME individuals (those whose gender is marked in the source sentence), will be marked with gender specified in the source in all translations. For a sentence with no AGMEs, there will only be one translation, and it will appear in the neutral column. 

Also note that if the neutral form of a noun is the most natural translation of the source, it will often appear in both 

## Labels:
**Positive Labels** — These labels all refer to sentences with AGMEs in test instances. In all cases, the individual’s gender it not marked in the source sentence:
target_only_gendered_pronoun - The target sentence refers to at least one AGME individual to by a gendered pronoun (but not a gendered noun) in the English translations. 

target_only_gendered_noun - The target sentence refers to at least one AGME individual to by a gendered noun (but not a gendered pronoun) in the English translations. 

target_only_gendered_noun+pronoun - The target sentence refers to at least one AGME individual to by both gendered nouns and pronouns.

**Negative Labels** - These all refer to non-AGME individuals in test instances. In all cases, the individual’s gender IS marked in the source (as well as the target).

source+target_gendered_noun - The target sentence refers to at least one individual by a gendered noun in the translation(s), and that individual was marked in the source sentence by a gendered noun. They are not referred to by gendered pronouns anywhere.


source+target_gendered_noun+pronoun - The target sentence refers to at least one individual by both gendered nouns and pronouns in the translation(s), and that individual was marked in the source sentence by a gendered noun. 


source_gendered_noun_target_pronoun - An individual was referred to by a gendered noun in the source sentence, but only by gendered pronouns in the translation(s). This case happen in exceptional circumstances I

**Other labels**

mixed - The instance contains a mixture of AGMEs and non-AGME individuals (who are marked for gender on source and target)

Multi - The instance contains more than one AGME.

Name - There is an AGME individual who is referred to by name (as well as other gender markers in the source). Not that proper names are treated as if they do not mark for gender.

non-AGME-name - A non-AGME individual is referred to by name. They need not be marked for gender anywhere; this simply indicates that a name appears somewhere in the translation(s)

N AGMEs (e.g. 0 AGMEs, 1 AGME, 2 AGMEs, etc…) - Indicates the number of AGMEs in the test instance.



