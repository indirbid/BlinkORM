<p class="has-line-data" data-line-start="0" data-line-end="2">BlinkORM – Blink-Fast PHP Active Record<br>
Blink once. Save forever. ⚡</p>
<p class="has-line-data" data-line-start="3" data-line-end="4">Ultra lightweight, modern Active Record implementation for PHP.</p>
<p class="has-line-data" data-line-start="5" data-line-end="6">Eloquent benzeri kullanım sunar ama çok daha az kod, sıfır bağımlılık ve maksimum hız ile.</p>
<p class="has-line-data" data-line-start="7" data-line-end="24">PHP 8.1+ (strict types + attributes)<br>
Sadece PDO kullanıyor — başka hiçbir şeye ihtiyaç yok<br>
#[Table] ve #[Column] attribute’ları ile deklaratif modeller<br>
Timestamps, soft deletes, fillable/guarded, casting, mutators/accessors kutudan çıkar<br>
Basit pagination, event sistemi, dirty checking<br>
Özellikler<br>
Attribute tabanlı tablo ve sütun tanımlama<br>
Otomatik created_at / updated_at<br>
Soft delete desteği (delete(), restore(), forceDelete(), withTrashed(), onlyTrashed())<br>
Veri tipleri casting (int, bool, datetime, array vs.)<br>
Accessor &amp; mutator desteği (getXAttribute, setXAttribute)<br>
Mass assignment koruması (fill() / forceFill())<br>
Global ve model bazlı event listener’lar<br>
find(), all(), paginate() yardımcı metodları<br>
Performans odaklı PDO wrapper (PdoDb)<br>
Kurulum<br>
Şu an Composer paketi henüz yayınlanmadı, ama çok yakında Packagist’te olacak.</p>
<p class="has-line-data" data-line-start="25" data-line-end="26">Şimdilik manuel kurulum:</p>
<p class="has-line-data" data-line-start="27" data-line-end="28">git clone <a href="https://github.com/indirbid/blinkorm.git">https://github.com/indirbid/blinkorm.git</a></p>
<h3 class="code-line" data-line-start=30 data-line-end=31 ><a id="Hzl_Balang_30"></a>Hızlı Başlangıç</h3>
<p class="has-line-data" data-line-start="32" data-line-end="33">&lt;?php</p>
<p class="has-line-data" data-line-start="34" data-line-end="35">use App\Models\User;</p>
<p class="has-line-data" data-line-start="36" data-line-end="38">// Veritabanı bağlantısını bir kere kur (genelde bootstrap veya index.php içinde)<br>
new PdoDb(‘localhost’, ‘root’, ‘’, ‘myapp’);</p>
<p class="has-line-data" data-line-start="39" data-line-end="49">// Model tanımı<br>
#[Table(‘users’)]<br>
class User extends Blink<br>
{<br>
protected array $fillable = [‘name’, ‘email’, ‘password’];<br>
protected array $hidden   = [‘password’];<br>
protected array $casts    = [<br>
‘is_active’ =&gt; ‘bool’,<br>
‘last_login’ =&gt; ‘datetime’,<br>
];</p>
<pre><code>// Mutator örneği
public function setPasswordAttribute(string $value): void
{
    $this-&gt;attributes['password'] = password_hash($value, PASSWORD_ARGON2ID);
}

// Accessor örneği
public function getFullNameAttribute(): ?string
{
    return $this-&gt;name ? $this-&gt;name . ' ✨' : null;
}
</code></pre>
<p class="has-line-data" data-line-start="61" data-line-end="63">}<br>
?&gt;</p>
<p class="has-line-data" data-line-start="64" data-line-end="70">// Kullanım örnekleri<br>
$user = new User();<br>
$user-&gt;name     = ‘Sanal’;<br>
$user-&gt;email    = ‘sanal@example.com’;<br>
$user-&gt;password = ‘gizli123’;<br>
$user-&gt;save();                  // ⚡ blink!</p>
<p class="has-line-data" data-line-start="71" data-line-end="75">// Bul ve güncelle<br>
$found = User::find(1);<br>
$found-&gt;name = ‘Sanal Yeni’;<br>
$found-&gt;save();</p>
<p class="has-line-data" data-line-start="76" data-line-end="81">// Sayfalama<br>
$paginated = User::paginate(15, 2);<br>
foreach ($paginated[‘data’] as $user) {<br>
echo $user-&gt;full_name . “\n”;<br>
}</p>
<p class="has-line-data" data-line-start="82" data-line-end="86">// Soft delete<br>
$user-&gt;delete();                        // soft delete<br>
User::withTrashed()-&gt;find($user-&gt;id);   // silinmiş kaydı getir<br>
$user-&gt;restore();                       // geri getir</p>
<p class="has-line-data" data-line-start="87" data-line-end="88">Neden BlinkORM?</p>
<p class="has-line-data" data-line-start="89" data-line-end="93">Hafif — Laravel Eloquent’tan ~15–20 kat daha az kod<br>
Modern — PHP 8+ attribute’ları ile temiz, deklaratif kod<br>
Hızlı — Gereksiz abstraction yok, direkt PDO ile çalışıyor<br>
Esnek — Mikroservislerden monolith projelere kadar her yere uyar</p>
<p class="has-line-data" data-line-start="94" data-line-end="95">Yakında Gelecek</p>
<p class="has-line-data" data-line-start="96" data-line-end="102">İlişkiler: hasOne, hasMany, belongsTo, belongsToMany<br>
Eager loading (with())<br>
Daha güçlü query scope’ları<br>
Composer paketi &amp; Packagist<br>
PHPUnit testleri<br>
Daha detaylı dokümantasyon</p>
<p class="has-line-data" data-line-start="103" data-line-end="110">Katkıda Bulunmak İster misin?<br>
PR’lar, issue’lar, öneriler çok değerli!<br>
Özellikle ilişkiler kısmı için yardıma açığım 😄<br>
MIT License — özgürce kullan, fork yap, değiştir, dağıt.<br>
BlinkORM ile kodla. Hızla.<br>
⭐ Vermeyi ve takip etmeyi unutma!<br>
<a href="https://github.com/indirbid/blinkorm">https://github.com/indirbid/blinkorm</a></p>
