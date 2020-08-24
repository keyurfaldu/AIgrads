## Climbing towards NLU: On Meaning, Form, and Understanding in the Age of Data
### Emily M. Bender, Alexander Koller
### ACL 2020

**Whats New**
This position paper analyses hindsight developments, and try to asssess is it the right direction by posing questions like, what is meaning in context of natural language, can a model which is only exposed to form ever learn meaning? whats possible way forward?

**Key Concepts**
* the language modeling task, because it only uses form as training data, cannot in principle lead to learning of meaning. 
* meaning to be the relation between a linguistic form and communicative intent.
* Authors defined "form" to be any observable realization of language.
* Authors defined meaning to be the relation between the form and something external to language
* Formally, meaning can be defined as relation M ⊆ E × I which contains pairs (e, i) of natural language expressions e and the communicative intents i they can be used to evoke
* Linguists distinguish communicative intent from conventional (or standing) meaning.
* Conventional meaning can be defined as C ⊆ E × S, which contains pairs (e, s) of expressions e and their conventional meanings s
* Thus, like the meaning relation M, C connects language to objects outside of language. Relation M, it is best understood as mediated by the relation C.
* The octopus test: 
    *  A and B, both fluent speakers of English, are independently stranded on two uninhabited islands. With an access to telegraph.
    * O, a hyper-intelligent deep-sea octopus who is unable to visit or observe the two islands, discovers a way to tap into the underwater cable and listen in on A and B’s conversations.
    * At some point, O starts feeling lonely. He cuts the underwater cable and inserts himself into the conversation, by pretending to be B and replying to A’s messages.
    * Now, A has invented a new device, say a coconut catapult. She excitedly sends detailed instructions on building a coconut catapult to B, and asks about B’s experiences and suggestions for improvements.
    * O decides to simply say “Cool idea, great job!”, A acceptsvthis reply as meaningful — but only because A does all the work in attributing meaning to O’s response.
    * A faces emergency, need B's help to create a new weapon. Would O be able to help?
    * Can O learn meaning?
* More constrained thought experiments:
    * Java: given access to just the java program, is it possible to learn JVM or compiler to produce output.
    * English: access to unlimited english texts, and unlabelled photos. Can model do task "count objects in the given photo?"

* Top-Down vs Bottom-Up approach, It would appear that we are making progress from Bottom-Up perspective? But are we progressing from Top-Down view?

* Can model also pass aditional data i.e. human interaction data, emotions data etc, which may help further to relate to external meaning.

