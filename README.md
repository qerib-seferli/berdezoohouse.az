# Bərdə ZOO House — PWA prototipi

## Başlatma
1. ZIP-i açın və faylları GitHub Pages repository-nin kökünə yükləyin.
2. GitHub Settings → Pages → Deploy from branch seçin.
3. `index.html` açın. İlk açılışda loqo və loading görünür.
4. **Demo rejimi** avtomatik işləyir: kataloq, səbət, sevimlilər, rayon üzrə çatdırılma, demo sifariş, WhatsApp mesajı, grooming sorğusu, admin məhsul və statusları. Demo məlumatları yalnız həmin brauzerdə localStorage-də saxlanır.
5. Admin: `index.html#admin` — **yalnız demo rejimində** açıqdır; real admin paneli hələ qoşulmayıb.

## Supabase
`supabase/migrations/001_initial.sql` faylını yeni layihədə SQL Editor-da işlətdikdən sonra `assets/js/config.js`-də Supabase URL və publishable/anon key daxil edilə bilər. **Diqqət:** bu, yalnız ilkin schema və auth/kataloq bağlantısıdır. Server Edge Functions tamamlanmadan real sifariş, admin dəyişiklikləri, rezervasiya və bank ödənişləri aktiv deyil. Təhlükəsizlik səbəbi ilə demo məlumatları real bazaya avtomatik köçürülmür.

### Admin təyinatı
Əvvəl `sehriyar@berdezoohouse.az` ünvanı ilə Supabase Auth hesabı yaradın və e-poçtu təsdiqləyin. Sonra SQL Editor-da (yalnız öz layihənizdə):
```sql
insert into public.admins(user_id)
select id from auth.users where lower(email)='sehriyar@berdezoohouse.az'
on conflict do nothing;
```
Bu addım admin rolunu bazaya yazır, lakin real admin UI/API əməliyyatları üçün ayrıca server funksiyaları lazımdır. **Email mətnini yox, auth user ID-ni səlahiyyətin əsası kimi istifadə edirik.**

## Gələcək istehsal işləri
- Auth profil redaktəsi, email verification, password reset callback və təhlükəsiz hesab silmə.
- Admin CRUD, media upload (bir şəkil), audit log, bütün istifadəçilərin səlahiyyətli oxunması.
- Server create-order / cancel-order (stok atomik rezervi, status tarixçəsi, qiymət və çatdırılma haqqının serverdə hesablanması).
- Grooming vaxt cədvəli, konfliktlərin qarşısı, server rezervasiyası.
- Kapital Bank merchant müqaviləsi və uyğun API ilə create-payment, callback verification, refund, reconciliation.
- Push subscription və server push göndərilməsi, cihaz testləri.
- Hüquqi mətnlər, canlı heyvan satışı qaydaları, real şəkillər, real məhsul məlumatları.

## Vizual fayllar
`assets/images/brand-logo.png` göndərilən loqodan hazırlanıb. PWA ikonları 16–512 px aralığında yaradılıb. Kateqoriya kiçik şəkilləri göndərilən UI/UX kollajından kəsilmiş **müvəqqəti vizuallardır**, real keyfiyyətli foto deyil. İstifadə üçün lisenziyalı foto və ya mağazanın öz şəkilləri ilə əvəz etmək lazımdır.

## Vacib
Bu ZIP tam məhsulun **işlək frontend prototipi və ilkin SQL skeletidir**, istehsala hazır təhlükəsiz e-commerce sistemi deyil. Demo qiymətlər və çatdırılma tarifləri nümunədir.
