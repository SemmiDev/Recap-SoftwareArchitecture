- mainstream = client -> shooping cart service -> order service -> payment service
	- problem = order lemot, solusi => node order service nya ditambah (misal 3). pertanyaanya bagaimana cara distribusiin dari shooping cart ke order nya
- perbaikan cara yg paling mudah  ==> menginstall proxy server, ex (nginx,apache httpd)
- jadinya = client -> shooping cart -> proxy server(distibusi ke order2 service) -> order service -> payment
	- problem = misal payment nya lemot, solusi = install beberapa node lagi
- pertanyaan nya bagaiaman cara order2 service dist juga ke payment nya = melalui proxy server
	- problem = app kita lemot banget (karena semua app kita melewati proxy server)
	- kita terlalu membebani proxy server, skenario terburuk if poxy nya down, app kita(yg di environemt itu ) juga akan down
- next solution = kita instal proxy sever di setiap service, jadinya
	shooping cart -> proxy server 1 -> service order1,order2,order3.
	order1,order2, dan order3 -> proxy server2 -> service payment1,payment2
- problem = misal proxy2 untuk payment nya mati, sekarang semua req ke payment gak ada yg jalan
- solusi lagi = tambah proxy server nya ke  masing2 service jadi dua, untuk order kasih 2 proxy ke paymeny juga kasih 2 proxy.
	- problem lagi = misal service nya bertambah otomatis kita juga akan menambah proxy nya, misal 10 service kita akan bikin 2 kali lipat proxy server nya.
	- problem = misal di kita ingin fast nih, keprluan nambah misal 4 node service order nya nah, kita harus setting lagi tuh proxy server nya, bikin team infra nya capek aja ya wkwkwkw
- nah solusi tersebut bisa kita atasi dengan service discovery
	- service discovery = mencari service secara otomatis di jaringan komputer
	- caranya = misal di conf file di shooping cart kita save address dari setiap order yg dibikin
	- dan di order sevice juga akan menyimpan address payment service nya

	- problem = payment nambah 1 node / 1 node mati, kita harus conf lagi tuh, bisa2 kita restart service2 nya untuk kembali melakukan configuration

- Solusi yg paling scalable untuk impement service discovery = install service registry ex : (Consul, Eureka)
- cara kerjanya =  service reg itu akan save semua daftar list of lokasi service dan endpoint2 nya
- nah ketika service2 saling menembah terlebihd dahulu dia akan bertanya kepada service registry
- pertanyaan nya akan lemot juga dong setiap service nanya dulu ke service reg nya, nah solusinya, si service jangan realtime nanya2 mulu, misal nanya sekali save bebrapa waktu kemudian baru nantinya nanya lagi (misal 5 atau 10 detik) baru nanya lagi takut ada perubahan
- misal service payment mati, nah biasanya kalau we use service registry mereka para service akan nanya nih, hei registry saya still life di alamat A misalnya.nah untuk itu service registry punya fitur yg bernama 'Health check'  untuk cek kesehatan service, misal tiap 5 detik dia akan cek secara berkala. jika tidak ada respon makan registry nanti akan di tandai sebagai bermasalah. nanti ada req dari order nanti req akan ditembak ke service paymen yg sehat.

= Di client harus implement 'client side load balancer / distribusi'

