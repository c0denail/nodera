# Nodera

Nodera, Windows sanal bilgisayarlarını kiralamak ve kendi bilgisayarınızın kaynaklarını paylaşmak için bir masaüstü uygulamasıdır. Kiralanan makine, kaynak sahibinin fiziksel bilgisayarında Hyper-V üzerinde çalışır. Kiracı, Windows masaüstünü Nodera içinden kullanır.

## İndir

| Platform | Kullanıcı sürümü |
| --- | --- |
| Windows x64 | [Nodera 0.5.15 sürüm sayfası](https://github.com/c0denail/nodera/releases/tag/v0.5.15) |
| macOS | Kiracı sürümü yakında yayımlanacak. |

Windows için sürüm sayfasındaki **Nodera_0.5.15_x64-setup.exe** dosyasını indirip çalıştırın. Aynı sayfada kurulum dosyasının SHA-256 sağlama toplamı bulunur. Hyper-V, kendi bilgisayarında sanal makine çalıştırıp kaynak paylaşacak kullanıcılar için gereklidir.

## Sanal bilgisayar kiralama

1. Nodera hesabınızla giriş yapın ve **Hazır sanal makineler** bölümünü açın. Müsait makineleri işlemci, RAM ve disk kapasitesine göre filtreleyebilirsiniz.
2. Uygun makineyi seçip kiralama başlatın. Merkezi hizmet makineyi oturumunuz için ayırır ve aynı anda ikinci bir rezervasyon yapılmasını engeller.
3. **Oturumlarım** bölümünden bağlanın. Windows masaüstü, kimliği doğrulanmış bir bağlantı üzerinden Nodera'nın içindeki Uzak Masaüstü (RDP) görüntüleyicisinde açılır. Kalan süreyi uygulamada görebilir ve kiralama devam ederken yeniden bağlanabilirsiniz.
4. Kiralama bittiğinde Windows oturum izni kaldırılır. Nodera, bir sonraki kiralama öncesinde sanal makinenin çalışma diskini temiz tabana döndürür. Kalıcı tutmak istediğiniz dosyaları oturum bitmeden kendi depolama alanınıza aktarın.

## Bilgisayarınızı paylaşıma açma

1. Hyper-V destekleyen bir Windows bilgisayarında **Kaynak paylaşımı** bölümünü açın ve ayırmak istediğiniz işlemci, RAM, disk ve ağ kaynaklarını belirleyin.
2. Hyper-V üzerinde ayrı bir Windows sanal makinesi oluşturun. Otomatik hazırlık akışı Windows kurulumunu, uzak masaüstünü, Active Directory bağlantısını ve temiz tabanı hazırlar.
3. Hazırlık tamamlanınca **Kiralamaya aç** seçeneğiyle ilanı yayımlayın. Kiralama sırasında uygulamalar ve dosyalar sanal makinenin çalışma diskinde kalır. Kaynak sahibinin bilgisayarı ve bağlantısı, makinenin erişilebilir olması için açık kalmalıdır.

## Active Directory ve bağlantı nasıl çalışır?

- **Nodera hesabı ve Windows hesabı:** Nodera hesabı üyelik ve rezervasyon için kullanılır. Active Directory ile hazırlanan makinelerde kiracının Nodera hesabı ayrı bir standart Windows etki alanı hesabıyla eşleştirilir.
- **Süreli erişim:** Etki alanına katılan sanal makinede uzak masaüstü izni yalnızca aktif kiracıya verilir. Kiracı standart kullanıcı yetkileriyle çalışır. Kiralama sona erince izin kaldırılır ve sonraki oturum için temiz bir çalışma ortamı hazırlanır.
- **Merkezi hizmet:** Node.js API'si ve MongoDB Atlas üyelik, ilan, rezervasyon ve oturum kayıtlarını yönetir. Sanal makine ve diskleri kaynak sahibinin bilgisayarında çalışır. RDP trafiği kimliği doğrulanmış WebSocket bağlantısı üzerinden taşınır.

## Uygulama Mağazası ve kurulum talepleri

Kiraladığınız Windows makinesinde yayımlanmış uygulamaları **Uygulama Mağazası** üzerinden kurabilirsiniz. Katalogdaki uygun paketler Microsoft WinGet'ten seçilir. Sanal makinedeki Nodera aracısı indirilen dosyanın SHA-256 değerini ve yayıncı imzasını doğrular. 0.5.15 ile uygun kurulumların sihirbazı aktif Windows oturumunda açılabilir. Destekleyen paketler arka planda da kurulabilir.

Mağazada bulunmayan bir EXE veya MSI için Windows'ta dosyaya sağ tıklayıp **Nodera ile kurulum talebi gönder** seçeneğini kullanabilirsiniz. Onaylanan kurulum sanal makinenin içinde çalışır ve kiracının hesabı standart kullanıcı olarak kalır.
