# BlinkORM – Blink-Fast PHP Active Record

**Blink once. Save forever.** ⚡

Ultra lightweight, modern **Active Record** implementation for PHP.

Eloquent benzeri kullanım sunar ama çok daha az kod, sıfır bağımlılık ve maksimum hız ile.

- PHP 8.1+ (strict types + attributes)
- Sadece **PDO** kullanıyor — başka hiçbir şeye ihtiyaç yok
- `#[Table]` ve `#[Column]` attribute'ları ile deklaratif modeller
- Timestamps, soft deletes, fillable/guarded, casting, mutators/accessors **kutudan çıkar**
- Basit pagination, event sistemi, dirty checking

### Özellikler

- Attribute tabanlı tablo ve sütun tanımlama
- Otomatik `created_at` / `updated_at`
- Soft delete desteği (`delete()`, `restore()`, `forceDelete()`, `withTrashed()`, `onlyTrashed()`)
- Veri tipleri casting (`int`, `bool`, `datetime`, `array` vs.)
- Accessor & mutator desteği (`getXAttribute`, `setXAttribute`)
- Mass assignment koruması (`fill()` / `forceFill()`)
- Global ve model bazlı event listener'lar
- `find()`, `all()`, `paginate()` yardımcı metodları
- Performans odaklı PDO wrapper (`PdoDb`)

### Kurulum

Şu an Composer paketi henüz yayınlanmadı, ama çok yakında Packagist'te olacak.

Şimdilik manuel kurulum:

```bash
git clone https://github.com/indirbid/blinkorm.git
