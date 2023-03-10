Exercice 1 
Modifiez la collection salle afin que soient dorénavant validés les documents destinés à y être insérés ; cette validation aura lieu en mode « strict » et portera sur les champs suivants :

nom sera obligatoire et devra être de type chaîne de caractères.

capacite sera obligatoire et devra être de type entier (int).

Dans le champ adresse, les champs codePostal et ville, tous deux de type chaîne de caractères, seront obligatoires.
```

```

Que constatez-vous lors de la tentative d’insertion suivante, et quelle en est la cause ?

```
db.salles.insertOne( 
{"nom": "Super salle", "capacite": 1500, "adresse": {"ville": "Musiqueville"}} 
) 
```
Le code postal est manquant alors qu'il est obligatoire pour l'insertion.

Que proposez-vous pour régulariser la situation ?

Il faut ajouter un code postal dans l'adresse, donc avoir cette insertion :
```
db.salles.insertOne( 
{"nom": "Super salle", "capacite": 1500, "adresse": {"codePostal": "69420", "ville": "Musiqueville"}} 
)
```

Exercice 2

Rajoutez à vos critères de validation existants un critère supplémentaire : le champ _id devra dorénavant être de type entier (int) ou ObjectId.
```
db.salles.createIndex(
   {
      "nom": 1,
      "capacite": 1,
      "adresse.codePostal": 1,
      "adresse.ville": 1,
      "_id": 1
   },
   {
      "unique": true,
      "partialFilterExpression": {
         "nom": { "$type": "string" },
         "capacite": { "$type": "int" },
         "adresse.codePostal": { "$type": "string" },
         "adresse.ville": { "$type": "string" },
         "_id": { "$type": "int"}
      }
   }
)
```

Que se passe-t-il si vous tentez de mettre à jour l’ensemble des documents existants dans la collection à l’aide de la requête suivante :

```
db.salles.updateMany({}, {$set: {"verifie": true}}) 
```

Supprimez les critères rajoutés à l’aide de la méthode delete en JavaScript


Exercice 3

Rajoutez aux critères de validation existants le critère suivant :

Le champ smac doit être présent OU les styles musicaux doivent figurer parmi les suivants : "jazz", "soul", "funk" et "blues".

Que se passe-t-il lorsque nous exécutons la mise à jour suivante ?


db.salles.update({"_id": 3}, {$set: {"verifie": false}}) 
