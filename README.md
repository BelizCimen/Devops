# Trendyol_Case1

#1.1
VM üzerinden centos kurulumu yaptım ve user'ı ilk kurulumda ekledim.Ardından "yum update" ile paket güncellemesi yaptım.

#1.2
Başlangıçta user girildiği için yeni bir user yaratmadım fakat bu user üzerinde işlem yapabilmek için "su beliz" komutuyla beliz isimli usera geçiş yaptım.

#1.3
Eklendiğim 10 gb'lık disk resimde görüldüğü üzere "/dev/sdb olarak" listelenmiştir.

![Screenshot (29)](https://user-images.githubusercontent.com/57073225/115946589-f70b6400-a4ca-11eb-8a9e-a2167b6bbf3f.png)

Ardından "fdisk /dev/sdb" komutu ile diskte partition oluşturuldu.Partition oluşturmak için bu komuttan sonra izlenmesi gereken adımlar:
  -yeni bir partition eklemek için "n" tuşuna basılır.
  -Bölümün primary olacağını belirtmek için "p" tuşuna basılır.
  -Bölüm numarası 1 olarak belirlenir.
  -Disk başlangıç ve bitiş değerini default olarak belirlemek için enter ile geçilir.
  -en sonunda "w" tuşu ile yapılan değişiklik partition tablosuna kaydedilir.

Sonrasında diski formatladım.Bunun için "sudo mkfs.ext3 /dev/sdb1" komutu kullandım.
"sudo mkdir bootcamp" ile mount edilecek kısmı belirttim.
Diski mount etmek için 
sudo mount /dev/sdb1 bootcamp/
(İlk denememde bu şekilde başarılı olamadım.Sorunu araştırırken mount işlemlerinde "sudo nano /etc/fstab" komutunun kullanıldığını öğrendim."sudo yum install nano" ile indirdikten sonra komutu çalıştırdığımda yeni arabellek'e geçildi uyarısı aldım.) 
"sudo nano /etc/fstab" komutunun sonraki line'ına yeni partition'umu mount edeceğim klasörü girdim. "/dev/sdb1    /home/beliz/bootcamp/    ext4  defaults 0 0" 
ardından mount -a komutunu çalıştırdım (bu komut /etc/fstab'ı Linux içinde reboot etmeden remountlamayı sağlıyor)

#bu kısımda https://askubuntu.com/questions/384062/how-do-i-create-and-tune-an-ext4-partition-from-the-command-line ve https://blog.narin.net.tr/centos-7-disk-mount-islemi-ve-yeniden-baslatildiginda-otomatik-mount-nasil-edilir/ kaynaklarından yararlandım)

#1.4
cd /opt
sudo mkdir bootcamp
cd bootcamp
sudo touch bootcamp.txt
sudo echo "merhaba trendyol" > bootcamp.txt 
bu işlemleri yaparken bootcamp.txt için erişim engeli aldım.Sebebini bulamadığımdan dolayı chown komutuyla işlem yapmaya devam ettim.
https://stackoverflow.com/questions/33703607/i-am-getting-unable-to-save-file-permission-denied-in-atom-when-saving-running/33839126
https://dev.to/kethmars/today-i-learned-permission-denied-chown-to-the-rescue-42gd

#1.5
"sudo chown beliz: bootcamp/; sudo find / -name "bootcamp.txt" -exec mv {} /home/beliz/bootcamp/ \;"  Yeniden erişim engeline takıldığım için chown komutu ekledikten sonra tek komutla bulunması istendiği için find ve move komutlarını birleştirdim.(https://stackoverflow.com/questions/22388480/how-to-pipe-the-results-of-find-to-mv-in-linux)

listelemek için "lsblk" komutunu kullandım.(https://askubuntu.com/questions/697767/listing-the-files-on-a-device-from-the-command-line)

![Screenshot (32)](https://user-images.githubusercontent.com/57073225/115952401-4e6efb80-a4ee-11eb-82a9-18bf7bfef308.png)

PS:Terminali türkçe yapma sebebim dili ingilizce yaptığımda klavyeyi tr'ye çevirmekte sorun yaşadım.Bu şekilde ilerlemek zorunda kaldım.

