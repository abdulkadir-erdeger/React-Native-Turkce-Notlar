# React Native Türkçe Notlar

## Mobil Programlama Nedir?
Mobil cihazlar için yazılım uygulamaları oluşturma sürecine mobil programlama diyoruz.

## Mobil Uygulama Geliştirmek için Hangi Seçenekler vardır?
Günümüzde üç çeşit mobil programlama geliştirme seçeneği mevcuttur.

![Resim 3](/gorsel/Resim3.png)

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

```javascript
//Bu şekildeki bir yapıyı...
React.createElement(
  MyButton,
  {color: 'blue', shadowSize: 2},
  'Click Me'
)

//Bu şekile çevirerek daha anlaşılır bir şekilde kullanmamızı sağlar.
<MyButton color="blue" shadowSize={2}>
  Click Me
</MyButton>
```

### Component 
React ve React Native dünyasınındaki her bir parçadır. Değer alabilen, aldığı değerleri işleyebilen özel yapılardır. Kullanıcı arayüzünü bağımsız, yeniden kullanılabilir parçalara ayırmanıza ve her bir parçayı ayrı ayrı düşünmenize olanak tanır. Kavramsal olarak componentler JavaScript fonksiyonları gibidir. Rastgele girdileri (props) kabul eder ve ekranda neyin görünmesi gerektiğini açıklayan React öğelerini döndürürler.
1.	**Functional Components**
> Fonksiyonel componentler daha basittir. Kendi durumlarını yönetmezler veya React Native tarafından sağlanan yaşam döngüsü yöntemlerine erişimleri yoktur. Tam anlamıyla eski JavaScript fonksiyonlarıdır ve bazen durumsuz bileşenler olarak da adlandırılırlar.

```javascript
import React from 'react';
import { Text } from 'react-native';

const App = () => {
  return (
    <Text>Merhaba Dünya</Text>
  );
}

export default App;
```

2.	**Class Components**
> Sınıf componentleri , React'in Component adlı bir temel sınıfını genişleten JavaScript ES2015 sınıflarıdır.  React yaşam döngüsü yöntemlerinin yanı sıra ana sınıftaki state/props işlevselliğine erişim sağlar.

```javascript
import React, { Component } from 'react';
import { Text } from 'react-native';

class App extends Component {
  render() {
    return (
      <Text>Merhaba Dünya</Text>
    );
  }
}

export default App;
```

### Props
Çoğu component oluşturulduklarında farklı parametrelerle özelleştirilebilir. Oluşturulan bu parametreler, özelliklerin kısaltması olan prop olarak adlandırılır. Props kullanarak verileri üst görünümden alt görünüme aktarabilirsiniz.

```javascript
<Button onPress={onPressFunction} title="Learn More" color="#841584" />
//Button component'ni incelersek burada onPress, title ve color props'larını özelleştirdik.

<MyComponent message="Merhaba Dünya" />
//Burada ise custom component olarak oluşturulmuş MyComponent bileşinine message prop'u oluşturarak "Merhaba Dünya" verisini aktardık.

```

### Style
React Native ile uygulamanızı JavaScript kullanarak şekillendirirsiniz. Tüm çekirdek bileşenler stil adında bir prop kabul eder. Stil adları ve değerleri genellikle CSS'in web'de nasıl çalıştığıyla eşleşir, ancak adlar camel casing kullanılarak yazılır, örneğin background-color yerine backgroundColor.

```javascript
import React from 'react';
import {Text, View } from 'react-native';

const App = () => {
    return (
      <View style={{marginTop:50}}>
        <Text style={{color:"red"}>just red</Text>
      </View>
    );
};

export default App;
```
>Bir bileşenin karmaşıklığı arttıkça, birkaç stili tek bir yerde tanımlamak için StyleSheet.create kullanmak genellikle daha temizdir.
```javascript
import React from 'react';
import { StyleSheet, Text, View } from 'react-native';

const App = () => {
    return (
      <View style={styles.container}>
        <Text style={styles.text}>just red</Text>
      </View>
    );
};

const styles = StyleSheet.create({
  container: {
    marginTop: 50,
  },
  text: {
    color: 'red',
  },
});

export default App;
```

### State
React ortamında değeri değiştiğinde tanımlaman componenti tekrar render etmesini sağlayan değişkenlere state adı verilir.

*  #### Class Component State Kullanımı
> React.Component’ini extend ettiği zaman React.Component’nin constructor’ı state’i componentimize tanımlar ve varsayılan değer olarak null atar. Daha sonrasında kendi state değerlerimizi belirlemek için componentimizin constructor’ında veya direkt olarak sınıf içerisinde tanımlamalarımızı gerçekleştirebiliriz.
Constructor içerisinde tanımlamış olduğumuz statelere erişmek için this ifadesini kullanırız.

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
> Class componentde React.Component içerisinde state mekanizması hazır olan bir yapıdan bileşenimizi türetiyorken functional component de bunu useState Hook ile sağlayabiliyoruz. useState bir dizi şeklinde tanımlanır iki parametre alır ilk parametre değişkenin (state) kendisi ikincisi değişiklikleri atamamızı sağlayan parametre olarak tanımlanır. 

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
- `componentDidMount()`
> Bileşen başlangıçta bir kez render edildiğinde çalışır.
-  `componentDidUpdate()`
> Bileşen update edildiğinde ait olduğu bileşen render edilir ve yenilenir.
-  `componentWillUnmount()`
> Bileşen yapıdan çıkarıldığında (silinmesi,gösterilmemesi) gibi durumlarda kullanılır .

React Hooks ile birlikte dünyamıza giren useEffect bu yapıları tek bir method altında kullanmamıza olanak sağlıyor.

- 
```javascript
useEffect (()=>{

},[])
```
> Bileşen başlangıçta bir kez render edildiğinde çalışır.
-  
```javascript
useEffect (()=>{

},[dependencies])
```
> Bileşen update edildiğinde ait olduğu bileşen render edilir ve yenilenir.
- 
```javascript
useEffect (()=>{ 

return()=>{}
},[])
```
> Bileşen yapıdan çıkarıldığında (silinmesi,gösterilmemesi) gibi durumlarda kullanılır .

### State Yönetimi
Veriler prop'lar aracılığıyla en üst componentden bir alt componenete (yukarıdan aşağıya) aktarılır. Ancak bu tür bir kullanım büyük bir uygulama içindeki birçok componenet arası veri aktarımı işlemi için zor ve kullanışsız bir yöntem olacaktır. Context ve Redux vb. yöntemler componentlerin her seviyesinden açıkça bir prop geçirmek zorunda kalmadan bileşenler arasında bu gibi değerleri paylaşmanın bir yolunu sağlar.

![Resim 4](/gorsel/Resim4.png)

1. **Context API**
> React’ın kendi geleneksel context yapısını kullanarak global bir state yönetimi tasarlamaya yöntemidir. Global state değerleri çok fazla değişmeyecekse, birden fazla context yapısı kullanacaksak bu yöntemi tercih edebiliriz.

2. **Redux**
> Redux state bileşenlerini yönetmemizi sağlayan kütüphanedir. Gloal statelerimizde sık sık veri güncellemesi yapacaksak, birden fazla reducer'a ihtiyaç duyacaksak bu yöntemi tercih edebiliriz. Redux’ta veri aktarımı ``Action``, ``Reducer`` ve ``Store`` gerçekleştirilir ve UI’a sunulur.

![Resim 5](/gorsel/Resim5.png)

* ``Action``
Actionlar içinde “type” isimli bir string değişkeni tutan bir Javascript nesnesidir. dispatch(action) fonksiyonu ile store içine aktarılır.

* ``Reducer``
Reducerlar, action sonucunda uygulamanın var olan state’i değiştirmesini sağlar. Uygulama değişikliğinin state’e aktarılması ise reducer tarafından olur.

* ``Store``
Store işlemi, action ve reducerı bir araya getirip yapıyı bağlar. Uygulamanın state’in tutulması, state’e erişim ``useSelector()``, state’in güncellenmesi ``useDispatch(action)`` gibi işlemler store üzerinden yönetilir.

* ``Provider``
Store’un tüm uygulamaya etki etmesini sağlayan, uygulamanın etrafını sarmalayan bir yapıdır.

### Memoization / Re-Render (Performans Optimizasyonu)
Bazen uygulamalarımızda fazla işlemci tüketen fonksiyonlar veya gereksiz re-render eden componentlerden kaynaklı performans sorunları yaşayabiliriz. Bu performans sorunlarını önlemek için Class componentler için ``Pure Component`` ve ``shouldComponentUpdate``, Functional componentler için ``useMome`` ve ``useCallback`` yöntemlerini kullanabiliriz.

* ``useMemo()``
> Fonksiyonlardaki fazla işlemci tüketen işlemler olduğu durumlarda fonksiyon her çağrıldığında bu işlemleri yapmak yerine fonksiyondan dönen son değeri afızasında tutar. Son değeri (dependency array) referans alarak son değer değişmedikçe cache deki değeri döndüren bir yöntemdir.


* ``useCallback()``
> Bir component her render edildiğinde component içerisindeki fonksiyonlarda da tekrardan oluşturulur. Bu da büyük projelerde component içerisindeki fonksiyonların tekrar tekar oluşturacağı için performans açısından kötü sonuçlar doğuracaktır. Bu re-render işlemini önlemek için useCallBack Hook'unu kullanıyoruz.

* ``memo``
> Bir üst component render edildiğinde ona bağlı alt componentlerde render olur. Alt componentlerde yansıyan herhangi bir değişlik yok ise boşa render işlemi gerçekleşmiş olur. React.memo ile sarmaladığımı bir component kendisine gönderilen props değerlerini saklar ve kaydeder. Bir sonraki render durumunda bu component’e gönderilen props değerleri,  bir önceki render edildiğindeki props değerleri ile karşılaştırır. Eğer props değerleri aynı ise componenti tekrar render etmez.

Özetle ``useMemo`` fonksiyondan dönen değeri, ``useCallback`` dönen fonksiyonu ve ``memo`` ise componentten dönen prop değerlerini hafızada tutarak gereksiz render işlemlerini önlememize yarıyor.
