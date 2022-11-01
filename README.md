# React Native Türkçe Notlar

## Mobil Programlama Nedir?
Mobil cihazlar için yazılım uygulamaları oluşturma sürecine mobil programlama diyoruz.

## Mobil Uygulama Geliştirmek için Hangi Seçenekler vardır?
Günümüzde üç çeşit mobil programlama geliştirme seçeneği mevcuttur.

- [ ] **Hybrid** 
> Tarayıcı motoru üzerinden derlenen uygulama geliştirme yöntemidir.
- [ ] **Native** 
> İşletim sistemi tarafından direkt derlenebilen uygulama geliştirme yöntemidir.
- [ ] **Cross Platfrom** 
> Bir Bridge ya da SDK aracılığıyla derlenen uygulama geliştirme yöntemidir.

## React Native Nedir?
React Native, hem IOS hem de Android işletim sistemleri için mobil uygulamalar geliştirmemizi sağlayan Javascript tabanlı bir Framework’tür.

## React Native Nasıl Çalışır?
React Native ile geliştirmiş bir uygulama Native uygulamaların aksine direk işletim sistemi tarafından değilde işletim sistemi üzerine inşa edilmiş Javascript motoru tarafından derlenir. Bu Javacript motoruna React Native Bridge diyoruz ve 3 ana bölümden oluşuyor.

![Resim 2](/gorsel/Resim2.png)

- [ ] **UI Thread** 
> Ekranda görüntülenecek bileşenlerin kontrolünü gerçekleştirir.
- [ ] **JS Thread** 
> Javascript ile geliştirilmiş tüm yapıların kontrolünü gerçekleştirir.
- [ ] **Native Thread** 
> Telefonun yerel bileşenlerine erişmek istediğimizdeki tüm sistemsel çağrıların kontrolünü gerçekleştirir.

## React Native Temelleri

### JSX (JavaScript Syntax Extension) 
React ve React Native ortamında programlama yaparken kullanılacak sözdiziminin okunmasını veya ifade edilmesini kolaylaştırmak için tasarlanmış formattır.

### Component 
React ve React Native dünyasınındaki her bir parçadır. Değer alabilen, aldığı değerleri işleyebilen özel yapılardır. Kullanıcı arayüzünü bağımsız, yeniden kullanılabilir parçalara ayırmanıza ve her bir parçayı ayrı ayrı düşünmenize olanak tanır. Kavramsal olarak componentler JavaScript fonksiyonları gibidir. Rastgele girdileri (props) kabul eder ve ekranda neyin görünmesi gerektiğini açıklayan React öğelerini döndürürler.
1.	**Functional Components**
> Fonksiyonel componentler daha basittir. Kendi durumlarını yönetmezler veya React Native tarafından sağlanan yaşam döngüsü yöntemlerine erişimleri yoktur. Tam anlamıyla eski JavaScript fonksiyonlarıdır ve bazen durumsuz bileşenler olarak da adlandırılırlar.
2.	**Class Components**
> Sınıf componentleri , React'in Component adlı bir temel sınıfını genişleten JavaScript ES2015 sınıflarıdır.  React yaşam döngüsü yöntemlerinin yanı sıra ana sınıftaki state/props işlevselliğine erişim sağlar.

### Props
Çoğu component oluşturulduklarında farklı parametrelerle özelleştirilebilir. Oluşturulan bu parametreler, özelliklerin kısaltması olan prop olarak adlandırılır. Props kullanarak verileri üst görünümden alt görünüme aktarabilirsiniz.

### Style
React Native ile uygulamanızı JavaScript kullanarak şekillendirirsiniz. Tüm çekirdek bileşenler style adında bir prop kabul eder. Stil adları ve değerleri genellikle CSS'in web'deki çalışma şekliyle eşleşir.

### State
React ortamında değeri değiştiğinde tanımlaman componenti tekrar render etmesini sağlayan değişkenlere state adı verilir.

*  #### Class Component State Kullanımı
<sub>React.Component’ini extend ettiği zaman React.Component’nin constructor’ı state’i componentimize tanımlar ve varsayılan değer olarak null atar. Daha sonrasında kendi state değerlerimizi belirlemek için componentimizin constructor’ında veya direkt olarak sınıf içerisinde tanımlamalarımızı gerçekleştirebiliriz.
Constructor içerisinde tanımlamış olduğumuz statelere erişmek için this ifadesini kullanırız.</sub>

```javascript
//State Tanımlama
constructor(props) {
   super(props);
   this.state = { myState: 'Merhaba React Native' };
}

//State değerini değiştirme
this.setState({myState: 'Merhaba Dünya'})
```
*  #### Function Component State Kullanımı
<sub>Class componentde React.Component içerisinde state mekanizması hazır olan bir yapıdan bileşenimizi türetiyorken functional component de bunu useState Hook ile sağlayabiliyoruz. useState bir dizi şeklinde tanımlanır iki parametre alır ilk parametre değişkenin (state) kendisi ikincisi değişiklikleri atamamızı sağlayan parametre olarak tanımlanır. </sub>

```javascript
//State Tanımlama
const [myState, setMyState]=useState("Merhaba React Native");

//State değerini değiştirme
setMyState('Merhaba Dünya')
```

### Lifecycle
Her componentin bir yaşam süreci vardır. Doğar, yaşar ve ölür. Biz geliştirme sürecinde bu componentlerin yaşam evrelerini lifecycle ile yönetiyoruz.

![Resim 1](/gorsel/Resim1.png)

React Hooks gelmeden önce Class component yapısında kullanılan üç aktif life-cycle method bulunmaktadır bunlar;
- [ ] `componentDidMount()`
> Bileşen başlangıçta bir kez render edildiğinde çalışır.
- [ ] `componentDidUpdate()`
> Bileşen update edildiğinde ait olduğu bileşen render edilir ve yenilenir.
- [ ] `componentWillUnmount()`
> Bileşen yapıdan çıkarıldığında (silinmesi,gösterilmemesi) gibi durumlarda kullanılır .

React Hooks ile birlikte dünyamıza giren useEffect bu yapıları tek bir method altında kullanmamıza olanak sağlıyor.

- [ ] `useEffect (()=>{},[])`
> Bileşen başlangıçta bir kez render edildiğinde çalışır.
- [ ] `useEffect (()=>{},[dependencies])`
> Bileşen update edildiğinde ait olduğu bileşen render edilir ve yenilenir.
- [ ] `useEffect (()=>{ return()=>{},[])`
> Bileşen yapıdan çıkarıldığında (silinmesi,gösterilmemesi) gibi durumlarda kullanılır .


