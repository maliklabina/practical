show dbs 

Online_Store> show collections

Online_Store> db.products.insertOne({ product_id: 101, name: "Wireless Mouse", category:
"Electronics", price: 899, stock: 50, brand: "LogiTech"})


Online_Store> db.products.find()


Online_Store> db.createCollection("customers", {
 validator: {
 $jsonSchema: {
 bsonType: "object",
 required: ["customer_id", "name", "email"],
 properties: {
 customer_id: { bsonType: "int" },
 name: { bsonType: "string" },
 email: { bsonType: "string" }
 }
 }
 } 
})

Online_Store> db.customers.insertOne({ customer_id: 1, name: "Riya Sharma", email:
"riya@gmail.com" })

Online_Store> db.products.find()

Online_Store> db.products.updateOne( { product_id: 101 }, { $set: { price: 999 }, $inc: { stock: -5 } })

Online_Store> db.products.find({product_id: 101})

Online_Store> db.products.updateOne({ product_id: 106 }, { $set: { name: "Earphones", category:
"Electronics", price: 499, stock: 40, brand: "BOAT" } }, { upupsert: true })


Online_Store> db.products.updateMany({ category: "Electronics" }, { $inc: { stock: 10
} })


Online_Store> db.products.find({ category: "Electronics" }).comment("Finding all Electronics items");

Online_Store> db.products.findOne({ product_id: 101 })

Online_Store> db.products.find({ price: { $gt: 1000 } })

Online_Store> db.products.find({ $or: [{ brand: "Sony" }, { brand: "Dell" }] })

Online_Store> db.products.find({ price: { $not: { $lt: 500 } } })

Online_Store> db.customers.find({ phone: null })

Online_Store> db.customers.updateOne({"customer_id":1},{$set:{ name: "Riya Sharma",email:
"riya@gmail.com", phone: 998283536}},{upsert:true})

Online_Store> db.customers.find({ phone: null })

Online_Store> db.orders.insertOne({ order_id: 5001, customer_id: 1, products: [101, 103, 105], 

Online_Store> db.orders.find({ products: 105 })

Online_Store> db.products.find({ $where: "this.price > 1000 && this.stock < 40" })

Online_Store> db.products.find().sort({ price: -1 }).skip(1).limit(3)

Online_Store> db.products.find().sort({ price: -1 }).skip(1).limit(1)
