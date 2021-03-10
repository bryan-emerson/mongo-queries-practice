# MongoDB CLI

## Getting Started

The prompts below each ask for you to write the query in MongoDB for performing
some action (described in the prompt). Your response should be a valid query and
it should be property formatted in Markdown. For example:

**Prompt:** Find all burgers in the `burgers` collection.

```
db.burgers.find({})
```

### Instructions

* Start your `mongo` server
* Connect to the `mongo` shell

### Prompts

**Prompt:** What is the command to start the `mongo` server?
```
brew services start mongodb-community@4.4
```

**Prompt:** What is the command to connect to the `mongo` shell?
```
mongo
```

**Prompt:** What is the command for listing all `mongo` databases?
```
show dbs
```

**Prompt:** What command would you use to create a database called `burgers`?
```
use burgers
```

**Prompt:** What command would you use to add the collection `burger` to your
`burgers` database?
```
db.burger.insert({...})
```

**Prompt:** What is the command for listing all collections in a database?
```
show collections
```

## Inserting

### Prompts

**Prompt:** Insert a single burger into the `burgers` collection with the
following:

* a `patty` property set to `beef`
* a `cheese` property set to `false`
* a `toppings` set to an array with `ketchup`, `onions`, and `pickles`

```
db.burger.insert({"name": "reg burg", "patty": "beef", "cheese": "false", "toppings": ["ketchup", "onions", "pickles"})
```

**Prompt:** Insert 10 burgers into the `burgers` collection with the following:

* a `patty` property that is set to one of: `beef`, `turkey`, or `veggie`
* a `cheese` property that is either `true` or `false`
* a `toppings` property that is either one of `ketchup`, `onions`, `pickles`,
  `mustard`, and `mayonnaise`
```
  db.burger.insertMany([
  {"name": "big burg", "patty": "beef", "cheese": "true", "toppings": ["ketchup", "mustard"]},
  {"name": "lil burg", "patty": "turkey", "cheese": "false", "toppings": ["ketchup", "mustard", "onions"]},
  {"name": "veg burg", "patty": "veggie", "cheese": "true", "toppings": ["ketchup", "mustard", "pickle"]},
  {"name": "extra big burg", "patty": "beef", "cheese": "true", "toppings": ["ketchup", "mustard", "onions"]},
  {"name": "big veg burg", "patty": "veggie", "cheese": "true", "toppings": ["ketchup", "mustard"]},
  {"name": "the burg", "patty": "beef", "cheese": "true", "toppings": ["ketchup", "mustard", "mayonnaise"]},
  {"name": "borger", "patty": "beef", "cheese": "false", "toppings": ["mustard", "pickles"]},
  {"name": "double borg", "patty": "beef", "cheese": "true", "toppings": ["ketchup", "mustard", "onions", "pickles"]},
  {"name": "rodeo burg", "patty": "turkey", "cheese": "true", "toppings": ["ketchup", "mustard", "onions"]},
  {"name": "hot burg", "patty": "veggie", "cheese": "true", "toppings": ["ketchup", "mustard", "pickles"]}])
  ```

## Reading

The following prompts will have you querying (reading) from your `burger`
collection. If you don't have burgers in your database that match the query
criteria described below, you wont get any results back. So, add one or two that
match that criteria before running the query.

### Prompts

**Prompt:** What query would find all burgers with a `beef` patty?
```
db.burger.find({}, {"patty": "beef"})
```

**Prompt:** What query would find all burgers with cheese on them?
```
db.burger.find({}, {"cheese": "true"})
```

**Prompt:** What query would find a burger by it's ObjectId?
```
db.burger.find({}, {"objectID": "1"})
```

**Prompt:** What query would find all burgers with `ketchup` as a topping?
```
db.burger.find({}, {"toppings": "ketchup"})

```

**Prompt:** What query would find all burgers with either a turkey or veggie
patty?
```
db.burger.find({patty:{$in:["turkey", "veggie"]}})
```

**Prompt:** What query would find all burgers with a beef patty and cheese?
```
db.burger.find({$and:[{"patty": "beef"}, {"cheese": "true"}]})
```

**Prompt:** What query would find all burgers with a beef patty and ketchup as
a topping?
```
db.burger.find({$and:[{"patty": "beef"}, {"toppings": "ketchup"}]})
```

**Prompt:** What query would find all burgers with a beef patty and both onions
and pickles as toppings?
```
db.burger.find({$and:
  [
    {"patty":"beef"},
    {"toppings":"pickles"},
    {"toppings":"onions"}
  ]
})
```



**Prompt:** What query would find burgers with either a turkey patty or cheese?
```
db.burger.find( { $or: [{"patty":"turkey"}, {"cheese":"true"}]})
```

## Update

### Prompts

**Prompt:** What query would update one burger by it's ObjectId, setting it's
"patty" to "pork"?

```
db.inventory.updateOne(
   { "_id": ObjectId("6048fd2e58b2028349dc2bac") },
   {
     $set: { "patty": "pork" },
   }
)
```

**Prompt:** What query would update all burgers with beef paddies to have
cheese? (i.e. set "cheese" to true)

```
db.inventory.updateMany(
   { "patty": "beef" },
   {
     $set: { "cheese": "true" },
     $currentDate: { lastModified: true }
   }
)
```

## Delete

### Prompts

**Prompt:** What query would delete a burger by it's ObjectId?

```
db.burger.remove({"_id": ObjectId("6048f81158b2028349dc2ba6")})
```

**Prompt:** What query would delete all veggie burgers?
```
db.inventory.deleteMany({"patty":"veggie"})
```

**Prompt:** What query would delete all burgers with pickles on them?

```
db.inventory.deleteMany({"toppings":"pickles"})
```
