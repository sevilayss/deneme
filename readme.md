erDiagram

  PERSONEL {
    int personel_id PK
    string adi
    string soyadi
    string tc_kimlik
    string sifre
    string telefon
    string email
    string gorevli_il
    string kadro_kurum
    int statu_id FK
    boolean aktif_mi
  }

  PERSONEL_STATU {
    int statu_id PK
    string statu_adi
    string statu_tanimi
  }

  KOORDINATORLUK {
    int koordinatorluk_id PK
    string koordinatorluk_adi
    string il
    int gorevli_koordinator_id FK
  }

  KOMISYON {
    int komisyon_id PK
    string komisyon_adi
    string il
    int bagli_koordinatorluk_id FK
  }

  KOMISYON_UYELIK {
    int id PK
    int komisyon_id FK
    int personel_id FK
    int statu_id FK
    date baslangic_tarihi
    date bitis_tarihi
    boolean aktif_mi
  }

  GOREV {
    int gorev_id PK
    string gorev_adi
    string gorev_tanimi
    date baslangic_tarihi
    date bitis_tarihi
    boolean aktif_mi
  }

  PERSONEL_GOREVLENDIRME {
    int id PK
    int personel_id FK
    int gorev_id FK
    date verilme_tarihi
    date teslim_tarihi
    boolean aktif_mi
  }

  KOMISYON_GOREVLENDIRME {
    int id PK
    int komisyon_id FK
    int gorev_id FK
    date verilme_tarihi
    date teslim_tarihi
    boolean aktif_mi
  }

  BRANCH {
    int branch_id PK
    string branch_name
    string description
    boolean status
  }

  PERSON_BRANCH {
    int id PK
    int personel_id FK
    int branch_id FK
    boolean is_primary
    datetime assigned_date
    int created_by
  }

  SOFTWARE {
    int software_id PK
    string software_name
    string category
    string description
    string logo_url
    boolean status
  }

  PERSON_SOFTWARE {
    int id PK
    int personel_id FK
    int software_id FK
    tinyint proficiency
    date last_used_date
    string note
    int created_by
    datetime created_at
  }

  UZMANLIK {
    int uzmanlik_id PK
    string uzmanlik_adi
    string uzmanlik_tanimi
    string kategori
    boolean aktif_mi
    date olusturma_tarihi
    date guncelleme_tarihi
  }

  PERSONEL_UZMANLIK {
    int id PK
    int personel_id FK
    int uzmanlik_id FK
    text aciklama
    boolean aktif_mi
    date baslangic_tarihi
    date bitis_tarihi
  }

  BECERI {
    int beceri_id PK
    string beceri_adi
    string beceri_tanimi
    string kategori
    boolean aktif_mi
    date olusturma_tarihi
    date guncelleme_tarihi
  }

  PERSONEL_BECERI {
    int id PK
    int personel_id FK
    int beceri_id FK
    text aciklama
    boolean aktif_mi
    date baslangic_tarihi
    date bitis_tarihi
  }

  %% İLİŞKİLER

  PERSONEL_STATU ||--o{ PERSONEL : "sahiptir"
  PERSONEL ||--o{ KOMISYON_UYELIK : "uye"
  KOMISYON ||--o{ KOMISYON_UYELIK : "icerir"

  KOORDINATORLUK ||--o{ KOMISYON : "bagli"
  PERSONEL ||--o{ KOORDINATORLUK : "koordinator olabilir"

  PERSONEL ||--o{ PERSONEL_GOREVLENDIRME : "gorevlendirilir"
  GOREV ||--o{ PERSONEL_GOREVLENDIRME : "atanir"

  KOMISYON ||--o{ KOMISYON_GOREVLENDIRME : "gorevlendirilir"
  GOREV ||--o{ KOMISYON_GOREVLENDIRME : "atanir"

  BRANCH ||--o{ PERSON_BRANCH : "kullanilir"
  PERSONEL ||--o{ PERSON_BRANCH : "branşa sahiptir"

  SOFTWARE ||--o{ PERSON_SOFTWARE : "kullanilir"
  PERSONEL ||--o{ PERSON_SOFTWARE : "program kullanir"

  UZMANLIK ||--o{ PERSONEL_UZMANLIK : "tanimlanir"
  PERSONEL ||--o{ PERSONEL_UZMANLIK : "uzmanliga sahiptir"

  BECERI ||--o{ PERSONEL_BECERI : "tanimlanir"
  PERSONEL ||--o{ PERSONEL_BECERI : "beceriye sahiptir"
