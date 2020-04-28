* Database scaling dipakai ketika database kita sudah cukup besar misal giga an sampai tera an
* Dua teknik database scaling = vertikal scaling dan horizontal scaling
	- Vertikal scaling = upgrade hardware nya(misal RAM, Hasdisk, CPU)  price huft :(
	- Horizontal scaling(reccomend) = beli hardware yg sama untuk nambah node/server yg baru. misal kita beli 4 buah hardisk2 yg murah untuk nambah node/server nya (sharding).
	 -problem = kalo kita insert data, akan dimasukkan ke database mana tuh? 
	atau select, dll...
	 -Solving = routing(motong2) data. untuk insert data pake algo sharding algorithm
	 	var hash = hashingAlgoritma(data,id);
	 	var shardNumber = hash % totalShard;
	 	database.save(data, shardNumber)

	 	- searching = lakuin searching di semua shard
	 	- paging = deep paging problem
	- misal 1 node mati, yg lain aman
	- mode replikasi data = 2x lipat sih dari total database heheh
	- replikasi di save di node yg berbeda
	- node master mati, node rep nya aman
	- ex --> mongo db, cassandra
- caching = biasanya dilakukan di ram/memory(kenceng hehe :) sebelum pake yg horizon(ribet) dan vertikal (mahal) , sebaiknya pake caching dulu.kalo sudah gk sanggup di handle di memory, bru reccomend pake vertikal / horizontal :)