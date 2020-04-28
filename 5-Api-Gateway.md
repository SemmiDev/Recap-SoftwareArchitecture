- Misal ada 3 buah sistem = inventory mobile, web, dan third party

- misal inventory web butuh inventory api dan sales api (conncet lebih dari 1 sistem)

- biasanya kita bedakan melalui url nya : 
	api.perusahaan.com/inventory
	api.perusahaan.com/payroll
	api.perusahaan.com/sales
	api.perusahaan.com/finance
	api.perusahaan.com/...
	
- bagaimana cara domain bisa nembak ke aplikasi lainnya ?
- biasanya melakukan routing seperti itu kita gunakan proxy server (nginx,apache httpd)
- itu merupakan salah satu konsep api gateway
- authentication (auth system) di setiap layer backend lebih baik dipindahkan ke api gateway
- di setiap authentication ada authorization( hak akses roles system (admin,finance,dll,) dan)
- salah satu fitur -> rate limite (menjaga backend service agar performa nya bagus), misal salah satu service yg hanya bisa nampung beberapa request per second. nah di api gateway di implement fitur rate limiter
- konsep implement lain = orchestrator. misal kita butuh 2 service sekaligus, ex : get employee sama get salary (cara biasa : pke hr api kemudina ->  payroll api). flow seperti ini akan membuat service saling ketergantungan.
- solve : kita implement orchestrator di api gateway, nanti api yg nembak ke service2 yg dibutuhkan
- standar api : misal disetiap backend return data2 yg beda2 misal ada json,xml,dll...
ketika kita expose keluar variasi dong dilihat user. kita bisa translae jadi satu mode. yaitu kita implement tranaslator di api gateway nya
- back end for frontend = misal kita bkin api di service untuk nge get data customer, setelah itu api akan bawa semua data customernya. pasti gede kan datnya trus time get nya lama juga kan :v misal ada batas bandwith2 di web. so, kita gak bisa tuh dari satu api di telen bulat2 untuk semua jenis client. biasanya kita bkin api buat masing2 device (web,mobile,third party system).
solve = konsep backend for frontend, kita bikin di apigateway, kita conf disana,misal di web, kita expose data yg diperlukan saja, begitupun di mobile dll.
yg lain bisa pake graph ql = get data separoh saja yg dibutuhkan, jangan semuanya. 

Kekurangan : jadi lebih lambat respon time nya(ada latency tambahan) karena ada layer2 di api gateway nya