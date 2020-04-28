Order service -> message broker -> notification service1 , notification service2 , notification service2 , notification service4 , dll.

si message broker secara pintar bisa mendistribusikan order2 yg dikirim dari order service kepadanya untuk didistribusika ke semua service, kalau hanya satu notif service akan lemot juga,  misal satu service hanya bisa get 1 request dari  message broker nah makanya dibuat banyak service.

jka tidak menggunakan message broker nanti si order service akan mengalami ketergantungan kepada notif service, jika seandainya notif service mati maka skenario terburuk nya order service juga akan mati.

disisi lain order service akan bergantung juga kepada message broker nah untuk itu kita harus pandai memilih teknologi message broker yang baik dan terpercaya : 
	1. Apache kafka (cocok untuk high traffic) = biaya besar karena harus run banyak node dalam sekali running.
	2. RabbitMQ (cocok untuk low - medium traffic) = running node tapi tidak sebanyak apache kafka.