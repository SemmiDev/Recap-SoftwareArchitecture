* ex in memory database : redis, memcache, dll
* web jsonwebtoken = http://jwt.io (reccomend menggunakan library yg sudah ada)
* JSON Web Token =  standard digunakan untuk menukarkan data antara dua pihak secara 	aman
* token = id / identitas khusus
* JSON WEB Token = semua identitas / informasi disisipkan di dalam tokennya
* JSON web token = terdiri dari string yg panjang yg terdiri dari 3 section 			yaitu Header,Payload,and Signature
	* Header => encode base 64 dari string data json, dalam string json kita masukan informasi algoritma untuk hashing nya (rem : hashing tidak bisa di decrypte lagi ya gak seperti encrypt)
	* Payload = base 64 dari json body, didalamnya kita masukin semua informasi yg kita butuh kirim yg bkin token ke service yg dituju, misal email,gender,name kita sisipkan dalam payload. (rem : informasi yg sensitif jangan kita masukkan, karena base 64 bisa di decode, likes : password)
	* Signature = String untuk melakukan verifikasi tokennya apakah valid atau tidak.
	hashing nya ini juga disisipi secret key. dan secret key ini harus di save disetiap service yg membutuhkan nya untuk verifikasi token.

	Flow ::
		1.	/Login ---> session service
		2.  session service akan mengembalikan JWT token(isinya username,misal email,dll) ---> 	/Login, yang akan di save di cookie
		3.  cookie yg berisi web token akan di sharing ke sevice lain
		4.  
			var jwtToken = httpRequest.cookie.token
			var payload  = JWT.verify(jwtToken, secretKey)
			var username = payload.username

* Kekurangan : proses melakukan verifikasi, sebelumnya kalau verifikasi kita call ke service lain / call ke database. nah kalau sekarang setiap service harus melakukan hashing menggunakan algoritma yg telah ditentukan, semakin susah algo nya, ketika hashing akan lama juga. 