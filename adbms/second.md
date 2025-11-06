test> show dbs


Aggregation: $match, $group, $lookup(Combining data from two different collections), $project(data
selection within single document)

Online_Store> db.orders.insertMany([ { order_id: 5001, customer_id: 1, total: 17000, status:
"Delivered", products: [101,105], date: ISODate("2025-09-10") }, 
])

Online_Store> db.orders.aggregate([ { $group: { _id: "$customer_id", total_spent: { $sum: "$total" } }
}])


Online_Store> db.orders.aggregate([ { $group: { _id: "$status", avg_order_value: { $avg: "$total" } }
}])



Online_Store> db.orders.aggregate([{ $match: { status: "Delivered" } }, { $group: {
_id: { month: { $month: "$date" } }, delivered_count: { $sum: 1 }} }])
[ { _id: { month: 9 }, delivered_count: 3 } ]
Online_Store> db.orders.aggregate([ { $lookup: { from: "customers",localField:
"customer_id", foreignField: "customer_id", as: "customer_info" } }, { $pro$project: {
order_id: 1, total: 1, "customer_info.name": 1 } }])




Online_Store> db.orders.aggregate([ { $sort: { total: -1 } }, { $limit: 3 }, { $project: { order_id: 1, total:
1, _id: 0 } }])


MapReduce: Calculate Total Revenue by Product
Online_Store> var mapFunction = function() { for (var i = 0; i < this.products.length; i++) {
emit(this.products[i], this.total);}};
Online_Store> var reduceFunction = function(productId, totals) { return Array.sum(totals);};
Online_Store> db.orders.mapReduce( mapFunction, reduceFunction, { out:
"product_revenue" })

Online_Store> db.product_revenue.find()

Online_Store> db.products.getIndexes()


Online_Store> db.products.dropIndex({ category: 1 })

Online_Store> db.products.createIndex({ category: 1, price: -1 }) category_1_price_-1
Online_Store> db.products.createIndex({ name: "text", brand: "text" }) name_text_brand_text
Online_Store> db.products.find({ $text: { $search: "Keyboard" } })

Online_Store> db.products.createIndex({ category: 1 }) category_1
Online_Store> db.products.find({ category: "Electronics"
}).explain("executionStats")

