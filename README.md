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


### Hızlı Başlangıç
<?php

use App\Models\User;

// Veritabanı bağlantısını bir kere kur (genelde bootstrap veya index.php içinde)
new PdoDb('localhost', 'root', '', 'myapp');

// Model tanımı
#[Table('users')]
class User extends Blink
{
    protected array $fillable = ['name', 'email', 'password'];
    protected array $hidden   = ['password'];
    protected array $casts    = [
        'is_active' => 'bool',
        'last_login' => 'datetime',
    ];

    // Mutator örneği
    public function setPasswordAttribute(string $value): void
    {
        $this->attributes['password'] = password_hash($value, PASSWORD_ARGON2ID);
    }

    // Accessor örneği
    public function getFullNameAttribute(): ?string
    {
        return $this->name ? $this->name . ' ✨' : null;
    }
}

###  Kullanım örnekleri
$user = new User();
$user->name     = 'Sanal';
$user->email    = 'sanal@example.com';
$user->password = 'gizli123';
$user->save();                  // ⚡ blink!

###  Bul ve güncelle
$found = User::find(1);
$found->name = 'Sanal Yeni';
$found->save();

###  Sayfalama
$paginated = User::paginate(15, 2);
foreach ($paginated['data'] as $user) {
    echo $user->full_name . "\n";
}

###  Soft delete
$user->delete();                        // soft delete
User::withTrashed()->find($user->id);   // silinmiş kaydı getir
$user->restore();                       // geri getir
Neden BlinkORM?

Hafif — Laravel Eloquent’tan ~15–20 kat daha az kod
Modern — PHP 8+ attribute'ları ile temiz, deklaratif kod
Hızlı — Gereksiz abstraction yok, direkt PDO ile çalışıyor
Esnek — Mikroservislerden monolith projelere kadar her yere uyar

### Yakında Gelecek

İlişkiler: hasOne, hasMany, belongsTo, belongsToMany
Eager loading (with())
Daha güçlü query scope'ları
Composer paketi & Packagist
PHPUnit testleri
Daha detaylı dokümantasyon

Katkıda Bulunmak İster misin?
PR'lar, issue'lar, öneriler çok değerli!
Özellikle ilişkiler kısmı için yardıma açığım 😄
MIT License — özgürce kullan, fork yap, değiştir, dağıt.
BlinkORM ile kodla. Hızla.
⭐ Vermeyi ve takip etmeyi unutma!
https://github.com/indirbid/blinkorm
