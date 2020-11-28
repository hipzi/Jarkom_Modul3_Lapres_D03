# Modul 3

 - DHCP 
	 * <a href="#soal-1">soal 1 </a>
	 * <a href="#soal-2">soal 2 </a>
	 * <a href="#soal-3-6">soal 3-6 </a>
 - Proxy 
	 * <a href="#soal-7">soal 7 </a>
	 * <a href="#soal-8-9">soal 8-9 </a>
	 * <a href="#soal-10">soal 10 </a>
     * <a href="#soal-11">soal 11 </a>
 - Testing
## DHCP
<justify>
<a id="soal-1"></a>
<p></p>
<p>1. Membuat topologi jaringan​ demi kelancaran TA-nya dengan kriteria sebagai berikut:</p>
<div style="width:60.1%">

![1.1](img/1-1.png)
</div>

![1.2](img/1-2.png)
</justify>

<justify>
<a id="soal-2"></a>
<p></p>
<p>2. SURABAYA ​ ditunjuk sebagai perantara (​ DHCP Relay​ ) antara DHCP Server dan client:</p>


![2.1](img/2-1.png)
<p>Kofigurasi isc-dhcp-relay pada Surabaya :</p>
<p>
    - <code>SERVERS</code> : Menuju IP Server DHCP Server, yaitu IP Mojokerto <br>
    - <code>INTERFACES</code> : Menuju interface client dan server <br>
</p>

![2.2](img/2-2.png)
<p>Kofigurasi isc-dhcp-relay pada Tuban (DHCP Server):</p>
<p>
    - <code>INTERFACES</code> : Interface pada tuban yang mengarah ke DHCP relay <br>
</p>

<p>Tambahkan konfigurasi pada DHCP Server agar mengenali topologi, dalam kasus ini <br> agar DHCP Server menemukan DHCP Relay dengan mengenalkan subnet yang berada diantaranya</p>

![2.3](img/2-3.png)
</justify>

<justify>
<a id="soal-3-6"></a>
<p></p>
<p>3. Client pada subnet 1 mendapatkan range IP dari 192.168.0.10 sampai 192.168.0.100 dan 192.168.0.110 sampai 192.168.0.200 </p>
<p>4. ​Client pada subnet 3 mendapatkan range IP dari 192.168.1.50 sampai 192.168.1.70 </p>
<p>5. ​Client mendapatkan DNS Malang dan DNS 202.46.129.2 dari DHCP </p>
<p>6. Client di subnet 1 mendapatkan peminjaman alamat IP selama 5 menit, sedangkan client pada subnet 3 mendapatkan peminjaman IP selama 10 menit. </p>

![3-6](img/3-6.png)

<p>Client pada Subnet 1 :</p>

![3.1](img/3-1.png)

![5.1](img/5-1.png)

![3.2](img/3-2.png)

![5.2](img/5-2.png)

<p>Client pada Subnet 2 :</p>

![4.1](img/4-1.png)

![5.3](img/5-3.png)

![4.2](img/4-2.png)

![5.4](img/5-4.png)
</justify>

## PROXY
<justify>
<a id="soal-7"></a>
<p></p>
<p>7. Membuat User autentikasi pada proxy:</p>

    htpasswd -c /etc/squid/passwd userta_d03
    pass : inipassw0rdta_d03
<p></p>

	mv /etc/squid/squid.conf /etc/squid/squid.conf.bak
	nano /etc/squid/squid.conf
<p></p>

    auth_param basic program /usr/lib/squid/ncsa_auth /etc/squid/passwd
	auth_param basic children 5
	auth_param basic realm Proxy
	auth_param basic credentialsttl 2 hours
	auth_param basic casesensitive on
	acl USERS proxy_auth REQUIRED

</justify>

<justify>
<a id="soal-8-9"></a>
<p></p>
<p>8. Membatasi penggunaan internet setiap hari ​Selasa-Rabu pukul 13.00-18.00​ untuk mengerjakan TA</p>
<p>9. Selasa-Kamis pukul 21.00 - 09.00 untuk bimbingan TA</p>

<p>Konfigurasi time pada squid</p>

![8,9](img/8-9.png)

    include /etc/squid/acl.conf

    http_access allow USERS PENGERJAAN_TA
	http_access allow USERS BIMBINGAN_TA
	http_access allow USERS BIMBINGAN_TA_2
</justify>

<justify>
<a id="soal-10"></a>
<p></p>
<p>10. Setiap mengakses google.com, maka akan di redirect menuju monta.if.its.ac.id​ agar Anri selalu ingat untuk mengerjakan TA</p>

	acl BLACKLISTS dstdomain google.com
	http_access deny BLACKLISTS
	deny_info http://monta.if.its.ac.id BLACKLISTS
</justify>

<justify>
<a id="soal-11"></a>
<p></p>
<p>10. Mengubah ​ error page default squid</p>

    cp -r ERR_ACCESS_DENIED /usr/share/squid/errors/English/ERR_ACCESS_DENIED
    
</justify>

<justify>
<a id="soal-12"></a>
<p></p>
<p>12. Domain proxy janganlupa-ta.d03.pw ​dan memasukkan port ​8080​</p>

<p>Buat DNS di Malang (DNS Server)</p>

![12.1](img/12-1.png)

![12.2](img/12-2.png)

<p>Konfigurasi DNS Forwarder agar bisa tetap terhubung ke internet</p>

![12.3](img/12-3.png)

<p>Tambahkan domain tersebut pada <code>visible_hostname</code> squid</p>

    http_port 8080
	visible_hostname janganlupa-ta.d03.pw
</justify>

<justify>
<p>Konfigurasi proxy (secara keseluruhan) :</p>

![proxy](img/proxy.png)
</justify>

## Testing
<justify>

![proxy](img/proxy-1.png)

![proxy](img/proxy-2.png)

![proxy](img/proxy-3.png)

![proxy](img/proxy-4.png)

<p>Ketika time di Mojokerto diubah menjadi Selasa pukul 15:00, saat mengakses google maka akan diarahkan ke monta seperti gambar dibawah ini :</p>

![proxy](img/proxy-5.png)
</justify>