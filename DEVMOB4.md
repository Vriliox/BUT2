# Syntaxe Swift

## Variables et Constantes

- **Variables** : Utilisez `var` pour déclarer une variable.
  ```swift
  var greeting = "Bonjour"
  greeting = "Salut"  // Vous pouvez changer la valeur d'une variable
  ```

- **Constantes** : Utilisez `let` pour déclarer une constante.
  ```swift
  let language = "Swift"
  // language = "Objective-C"  // Erreur : ne peut pas changer la valeur d'une constante
  ```

## Types de Données

- **Int** : Entiers
  ```swift
  var age: Int = 25
  ```

- **Double** et **Float** : Nombres à virgule flottante
  ```swift
  var pi: Double = 3.14
  var temperature: Float = 22.5
  ```

- **String** : Chaînes de caractères
  ```swift
  var name: String = "Alice"
  ```

- **Bool** : Valeurs booléennes
  ```swift
  var isSwiftFun: Bool = true
  ```

## Opérateurs

- **Opérateurs arithmétiques** : `+`, `-`, `*`, `/`, `%`
  ```swift
  let sum = 5 + 3
  let difference = 10 - 2
  ```

- **Opérateurs de comparaison** : `==`, `!=`, `>`, `<`, `>=`, `<=`
  ```swift
  let isEqual = (5 == 3)  // false
  ```

## Structures de Contrôle

- **Conditionnelles** : `if`, `else if`, `else`
  ```swift
  let temperature = 25
  if temperature > 30 {
      print("Il fait chaud !")
  } else if temperature > 20 {
      print("Il fait bon.")
  } else {
      print("Il fait froid.")
  }
  ```

- **Boucles** : `for-in`, `while`, `repeat-while`
  ```swift
  for i in 1...5 {
      print(i)
  }

  var count = 0
  while count < 5 {
      print(count)
      count += 1
  }
  ```

## Fonctions

- **Déclaration de fonction**
  ```swift
  func greet(name: String) -> String {
      return "Bonjour, \(name) !"
  }

  let greeting = greet(name: "Bob")
  ```

## Collections

### Tableaux (Arrays)

```
var fruits = ["Pomme", "Banane", "Cerise"]
```

- **Ajouter un élément** : Utilisez `append(_:)` pour ajouter un élément à la fin du tableau.
  ```
  fruits.append("Orange")
  ```

- **Accéder à un élément** : Utilisez l'index pour accéder à un élément spécifique.
  ```
  let firstFruit = fruits[0]  // "Pomme"
  ```

- **Modifier un élément** : Utilisez l'index pour modifier un élément existant.
  ```
  fruits[1] = "Poire"
  ```

- **Supprimer un élément** : Utilisez `remove(at:)` pour supprimer un élément à un index spécifique.
  ```
  fruits.remove(at: 2)
  ```

- **Compter les éléments** : Utilisez la propriété `count` pour obtenir le nombre d'éléments.
  ```
  let numberOfFruits = fruits.count
  ```

- **Itérer sur un tableau** : Utilisez une boucle `for-in` pour parcourir les éléments.
  ```
  for fruit in fruits {
      print(fruit)
  }
  ```

### Dictionnaires

```
var capitales = ["France": "Paris", "Espagne": "Madrid"]
```

- **Ajouter ou modifier une paire clé-valeur** : Utilisez la syntaxe de sous-script pour ajouter ou modifier une valeur.
  ```
  capitales["Italie"] = "Rome"
  ```

- **Accéder à une valeur** : Utilisez la clé pour accéder à la valeur associée.
  ```
  if let capitaleFrance = capitales["France"] {
      print(capitaleFrance)  // "Paris"
  }
  ```

- **Supprimer une paire clé-valeur** : Utilisez `removeValue(forKey:)` pour supprimer une paire.
  ```
  capitales.removeValue(forKey: "Espagne")
  ```

- **Compter les paires** : Utilisez la propriété `count` pour obtenir le nombre de paires clé-valeur.
  ```
  let numberOfCapitales = capitales.count
  ```

- **Itérer sur un dictionnaire** : Utilisez une boucle `for-in` pour parcourir les paires clé-valeur.
  ```
  for (pays, capitale) in capitales {
      print("\(capitale) est la capitale de \(pays).")
  }
  ```

## Optionnels

- **Optionnels** : Utilisés pour gérer l'absence de valeur
  ```swift
  var optionalName: String? = "Alice"
  if let name = optionalName {
      print("Bonjour, \(name) !")
  } else {
      print("Pas de nom disponible.")
  }
  ```

## Classes et Objets

- **Classe** : Un plan pour créer des objets. Une classe encapsule des données pour l'état (propriétés) et des comportements (méthodes).

  ```swift
  class Animal {
      var name: String
      var age: Int

      init(name: String, age: Int) {
          self.name = name
          self.age = age
      }

      func makeSound() {
          print("\(name) fait un son.")
      }
  }
  ```

- **Objet** : Une instance d'une classe.

  ```swift
  let myPet = Animal(name: "Rex", age: 3)
  myPet.makeSound()  // Affiche : "Rex fait un son."
  ```

## Héritage

- **Héritage** : Une classe peut hériter des propriétés et des méthodes d'une autre classe.

  ```swift
  class Dog: Animal {
      func fetch() {
          print("\(name) va chercher la balle.")
      }
  }

  let myDog = Dog(name: "Buddy", age: 2)
  myDog.makeSound()  // Hérité de la classe Animal
  myDog.fetch()      // Méthode spécifique à la classe Dog
  ```

## Polymorphisme

- **Polymorphisme** : La capacité de traiter des objets de différentes classes à travers une interface commune.

  ```swift
  let animals: [Animal] = [myPet, myDog]

  for animal in animals {
      animal.makeSound()  // Appelle makeSound() sur chaque objet
  }
  ```

## Encapsulation

- **Encapsulation** : Restreindre l'accès direct à certaines composantes d'un objet, ce qui est réalisé en utilisant des niveaux d'accès comme `private` et `public`.

  ```swift
  class Car {
      private var speed: Int = 0

      func accelerate() {
          speed += 10
          print("Vitesse actuelle : \(speed) km/h")
      }
  }

  let myCar = Car()
  myCar.accelerate()  // Affiche : "Vitesse actuelle : 10 km/h"
  // myCar.speed  // Erreur : 'speed' est privé
  ```

# Fonctions de base pour une application iOS avec Storyboard


## Configuration de l'Interface Utilisateur

- **Lier une IBAction à un bouton** : Pour gérer les actions lorsqu'un bouton est cliqué.
  ```swift
  @IBAction func buttonTapped(_ sender: UIButton) {
      print("Bouton cliqué !")
  }
  ```

- **Lier une IBOutlet à un label** : Pour mettre à jour le texte d'un label.
  ```swift
  @IBOutlet weak var welcomeLabel: UILabel!

  func updateLabelText() {
      welcomeLabel.text = "Bienvenue dans mon application !"
  }
  ```

## Gestion des Données Utilisateur

- **Stocker des données avec UserDefaults** : Sauvegarder des données simples.
  ```swift
  func saveUserName(name: String) {
      UserDefaults.standard.set(name, forKey: "userName")
  }

  func getUserName() -> String? {
      return UserDefaults.standard.string(forKey: "userName")
  }
  ```

## Utilisation des Alertes

- **Afficher une alerte** : Montrer un message d'alerte à l'utilisateur.
  ```swift
  func showAlert() {
      let alert = UIAlertController(title: "Attention", message: "Ceci est une alerte.", preferredStyle: .alert)
      alert.addAction(UIAlertAction(title: "OK", style: .default, handler: nil))
      present(alert, animated: true, completion: nil)
  }
  ```

# Lecture de Fichiers XML en Swift

La lecture de fichiers XML est une compétence utile pour traiter des données structurées dans une application iOS. Voici comment vous pouvez lire un fichier XML en Swift.

## Exemple de Lecture de Fichier XML

- **Utilisation de `XMLParser`** : Pour analyser un fichier XML.

  ```swift
  import Foundation

  class XMLParserDelegate: NSObject, XMLParserDelegate {
      var currentElement = ""
      var currentValue = ""
      var dataDictionary = [String: String]()

      func parser(_ parser: XMLParser, didStartElement elementName: String, namespaceURI: String?, qualifiedName qName: String?, attributes attributeDict: [String : String] = [:]) {
          currentElement = elementName
      }

      func parser(_ parser: XMLParser, foundCharacters string: String) {
          currentValue += string
      }

      func parser(_ parser: XMLParser, didEndElement elementName: String, namespaceURI: String?, qualifiedName qName: String?) {
          if !currentValue.isEmpty {
              dataDictionary[currentElement] = currentValue
              currentValue = ""
          }
      }
  }

  func parseXML(from fileURL: URL) {
      let parser = XMLParser(contentsOf: fileURL)!
      let delegate = XMLParserDelegate()
      parser.delegate = delegate
      parser.parse()

      // Utiliser les données analysées
      print(delegate.dataDictionary)
  }

  // Exemple d'utilisation
  if let xmlFileURL = Bundle.main.url(forResource: "data", withExtension: "xml") {
      parseXML(from: xmlFileURL)
  }
  ```

## Explications

- **XMLParserDelegate** : Une classe qui implémente les méthodes nécessaires pour gérer les événements de l'analyseur XML.
- **parser(_:didStartElement:...)**: Appelée lorsque l'analyseur rencontre une balise d'ouverture.
- **parser(_:foundCharacters:)** : Appelée lorsque l'analyseur trouve du texte entre les balises.
- **parser(_:didEndElement:...)** : Appelée lorsque l'analyseur rencontre une balise de fermeture.