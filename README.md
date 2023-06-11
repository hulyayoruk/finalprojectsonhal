class DepremDestekSistemi:
    def __init__(self):
        self.yemek_fiyatlari = {
                            
            'et': 79,
            'köfte': 75,
            'tavuk': 65,
            'sebze': 50
        }
        self.indirim_oranlari = {
            5: 0.3,
            10: 0.4
        }
        self.bagis_fonu = 0

    def basla(self):
        print("Deprem Destek Sistemine Hoş Geldiniz!")
        while True:
            secim = input("Giriş yapmak için '1' tuşuna, çıkmak için 'q' tuşuna basın: ")
            if secim == '1':
                self.giris_sayfasi()
            elif secim.lower() == 'q':
                print("Sistemden çıkılıyor...")
                break
            else:
                print("Geçersiz bir seçim yaptınız.")

    def giris_sayfasi(self):
        print("Giriş sayfasına hoş geldiniz!")
        while True:
            secim = input("Kullanıcı olarak giriş yapmak için '1', admin olarak giriş yapmak için '2', çıkış yapmak için 'q' tuşuna basın: ")
            if secim == '1':
                self.kullanici_giris()
            elif secim == '2':
                self.admin_giris()
            elif secim.lower() == 'q':
                print("Giriş sayfasından çıkılıyor...")
                break
            else:
                print("Geçersiz bir seçim yaptınız.")

    def kullanici_giris(self):
        print("Kullanıcı olarak giriş yapıyorsunuz.")
        ad_soyad = input("Adınız ve soyadınızı girin: ")
        secim = input("Yemek siparişi vermek için '1', bağış yapmak için '2' tuşuna basın: ")

        if secim == '1':
            self.yemek_siparisi(ad_soyad)
        elif secim == '2':
            self.bagis_yap(ad_soyad)
        else:
            print("Geçersiz bir seçim yaptınız.")

    def admin_giris(self):
        print("Admin olarak giriş yapıyorsunuz.")
        sifre = input("Admin şifresini girin: ")

        if sifre == 'admin':
            self.admin_paneli()
        else:
            print("Geçersiz şifre!")

    def yemek_siparisi(self, ad_soyad):
        print("Yemek siparişi veriliyor...")
        yas = int(input("Yaşınızı girin: "))
        if yas < 16:
            print("Yaşınız 16'dan küçük olduğu için sistemden yemek siparişi veremezsiniz.")
            return

        kisi_sayisi = int(input("Kaç kişilik yemek siparişi vermek istiyorsunuz? "))
        toplam_tutar = self.yemek_fiyatlari_secimi() * kisi_sayisi

        indirim_orani = self.indirim_orani_hesapla(kisi_sayisi)
        toplam_tutar -= toplam_tutar * indirim_orani

        print("Toplam tutar: ", toplam_tutar)
        self.odeme_sayfasi(toplam_tutar)

    def odeme_sayfasi(self, tutar):
        print("Ödeme sayfasına yönlendiriliyorsunuz...")
        odeme_secim = input("Ödeme yapmak için '1', iptal etmek için '2' tuşuna basın: ")

        if odeme_secim == '1':
            print("Ödeme işlemi tamamlandı.")
            self.fatura_sayfasi(tutar)
        elif odeme_secim == '2':
            print("Ödeme işlemi iptal edildi.")
        else:
            print("Geçersiz bir seçim yaptınız.")

    def fatura_sayfasi(self, tutar):
        print("Fatura sayfası")
        print("**********************************")
        print("              Fatura              ")
        print("**********************************")
        print("Toplam Tutar: ", tutar)
        print("Ödeme Tarihi: 11/06/2023")
        print("**********************************")
        print("         Teşekkür ederiz!         ")
        print("**********************************")

    def yemek_fiyatlari_secimi(self):
        print("Yemek seçimi yapınız:")
        print("1. Et Menü")
        print("2. Köfte Menü")
        print("3. Tavuk Menü")
        print("4. Sebze Menü")
        secim = int(input("Seçiminizi yapın (1-4): "))

        if secim == 1:
            return self.yemek_fiyatlari['et']
        elif secim == 2:
            return self.yemek_fiyatlari['köfte']
        elif secim == 3:
            return self.yemek_fiyatlari['tavuk']
        elif secim == 4:
            return self.yemek_fiyatlari['sebze']
        else:
            print("Geçersiz bir seçim yaptınız.")
            return 0

    def indirim_orani_hesapla(self, kisi_sayisi):
        indirim_orani = 0
        for kisi_say, indirim in self.indirim_oranlari.items():
            if kisi_sayisi > kisi_say:
                indirim_orani = indirim
        return indirim_orani

    def bagis_yap(self, ad_soyad):
        print("Bağış yapılıyor...")
        miktar = float(input("Bağış miktarını girin: "))
        self.bagis_fonu += miktar
        print("Bağışınız alınmıştır. Teşekkür ederiz!")

    def admin_paneli(self):
        print("Admin Paneline Hoş Geldiniz!")
        while True:
            secim = input("Yemek fiyatlarını güncellemek için '1', indirim oranlarını güncellemek için '2', bağış fonunu güncellemek için '3', çıkış yapmak için 'q' tuşuna basın: ")
            if secim == '1':
                self.yemek_fiyatlari_guncelle()
            elif secim == '2':
                self.indirim_oranlari_guncelle()
            elif secim == '3':
                self.bagis_fonu_guncelle()
            elif secim.lower() == 'q':
                print("Admin Panelinden çıkılıyor...")
                break
            else:
                print("Geçersiz bir seçim yaptınız.")

    def yemek_fiyatlari_guncelle(self):
        print("Yemek fiyatlarını güncelleyin:")
        print("1. Et Menü - Şuanki fiyat:", self.yemek_fiyatlari['et'])
        print("2. Köfte Menü - Şuanki fiyat:", self.yemek_fiyatlari['köfte'])
        print("3. Tavuk Menü - Şuanki fiyat:", self.yemek_fiyatlari['tavuk'])
        print("4. Sebze Menü - Şuanki fiyat:", self.yemek_fiyatlari['sebze'])
        secim = int(input("Güncellemek istediğiniz menü numarasını girin (1-4): "))
        fiyat = float(input("Yeni fiyatı girin: "))

        if secim == 1:
            self.yemek_fiyatlari['et'] = fiyat
        elif secim == 2:
            self.yemek_fiyatlari['köfte'] = fiyat
        elif secim == 3:
            self.yemek_fiyatlari['tavuk'] = fiyat
        elif secim == 4:
            self.yemek_fiyatlari['sebze'] = fiyat
        else:
            print("Geçersiz bir seçim yaptınız.")

        print("Yemek fiyatları güncellendi.")

    def indirim_oranlari_guncelle(self):
        print("Indirim oranlarını güncelleyin:")
        for kisi_say, indirim in self.indirim_oranlari.items():
            print(f"{kisi_say} kişi üzerine {indirim*100}% indirim")
        kisi_say = int(input("Güncellemek istediğiniz kişi sayısını girin: "))
        indirim_orani = float(input("Yeni indirim oranını girin (0-1): "))

        self.indirim_oranlari[kisi_say] = indirim_orani
        print("Indirim oranları güncellendi.")

    def bagis_fonu_guncelle(self):
        print("Bağış fonunu güncelleyin:")
        print("Mevcut bağış fonu miktarı:", self.bagis_fonu)
        miktar = float(input("Yeni bağış fonu miktarını girin: "))
        self.bagis_fonu = miktar
        print("Bağış fonu güncellendi.")


# Kullanım örneği
sistem = DepremDestekSistemi()
sistem.basla()
