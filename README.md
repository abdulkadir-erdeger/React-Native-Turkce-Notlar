# React Native Türkçe Notlar

<!--ts-->
- [Mobil Programlama Nedir?](#mobil-programlama-nedir)
- [Mobil Uygulama Geliştirmek için Hangi Seçenekler vardır?](#mobil-uygulama-geliştirmek-için-hangi-seçenekler-vardır)
- [React Native Nedir?](#react-native-nedir)
- [React Native Nasıl Çalışır?](#react-native-nasıl-çalışır)
  - [Eski Mimari](#eski-mimari)
  - [Yeni Mimari](#yeni-mimari)
- [React Native Proje Oluşturma Yaklaşımları](#react-native-proje-oluşturma-yaklaşımları)
	- [Expo Go / EAS vs React Native CLI](#expo-go--eas-vs-react-native-cli)
	- [Proje Oluşturma Adımları](#proje-oluşturma-adımları)
- [React Native Temelleri](#react-native-temelleri)
	- [JSX (JavaScript Syntax Extension)](#jsx-javascript-syntax-extension)
	- [Component](#component)
		- [Functional Components](#functional-components)
		- [Class Components](#class-components)
	- [Props](#props)
	- [Style](#style)
	- [State](#state)
		- [Class Component State Kullanımı](#class-component-state-kullanımı)
		- [Function Component State Kullanımı](#function-component-state-kullanımı)
	- [Lifecycle](#lifecycle)
		- [Class Component Lifecycle](#class-component-lifecycle)
		- [Functional Component Hook Lifecycle](#functional-component-hook-lifecycle)
	- [State Yönetimi](#state-yönetimi)
		- [Context API](#context-api)
		- [Redux](#redux)
		- [Redux Saga](#redux-saga)
	- [Memoization / Re-Render (Performans Optimizasyonu)](#memoization--re-render-performans-optimizasyonu)
		- [`useMemo()`](#usememo)
		- [`useCallback()`](#usecallback)
		- [`memo`](#memo)
	- [Test İşlemleri](#test-i̇şlemleri)
		- [Unit Test](#unit-test)
			- [Unit Test Araçları](#unit-test-araçları)
			- [Snapshots Testi](#snapshots-testi)
			- [Component Testi](#component-testi)
			- [Fonksiyon Testi](#fonksiyon-testi)
			- [Stil Testi](#stil-testi)
		- [Integration Testi](#integration-testi)
		- [End to End Testi](#end-to-end-testi)
- [React Native Yayınlama Süreçleri (Deployment)](#react-native-yayınlama-süreçleri-deployment)
	- [Android Yayınlama Süreci (Google Play Store)](#android-yayınlama-süreci-google-play-store)
	- [iOS Yayınlama Süreci (Apple App Store)](#ios-yayınlama-süreci-apple-app-store)
	- [OTA (Over-The-Air) Güncellemeler](#ota-over-the-air-güncellemeler)
- [Sık Kullanılan Komutlar (CLI / Expo)](#sık-kullanılan-komutlar-cli--expo)
- [Proje Yükseltme (Upgrade)](#proje-yükseltme-upgrade)
	- [React Native CLI Yükseltme](#react-native-cli-yükseltme)
	- [Expo Yükseltme](#expo-yükseltme)

<!--te-->

## Mobil Programlama Nedir?
Mobil cihazlar (akıllı telefonlar, tabletler) için yazılım uygulamaları oluşturma sürecine mobil programlama diyoruz.

## Mobil Uygulama Geliştirmek için Hangi Seçenekler vardır?
Günümüzde üç ana mobil uygulama geliştirme yaklaşımı mevcuttur:

![Resim 3](/gorsel/Resim3.png)

- [ ] **Hybrid** 
> Web teknolojileri (HTML, CSS, JS) ile yazılan ve bir WebView (tarayıcı motoru) içinde derlenerek çalışan uygulamalardır (Örn: Ionic, Capacitor).
- [ ] **Native** 
> Doğrudan hedef platformun kendi dili ve SDK'sı ile geliştirilen uygulamalardır (iOS için Swift/Objective-C, Android için Kotlin/Java).
- [ ] **Cross Platfrom** 
> Tek bir kod tabanı yazarak bir Köprü (Bridge), C++ Arayüzü (JSI) veya özel bir Rendering Engine/SDK aracılığıyla her iki platforma da çıktı veren geliştirme yöntemidir (Örn: React Native, Flutter).

## React Native Nedir?
React Native, Meta (Facebook) tarafından geliştirilen; JavaScript ve React prensiplerini kullanarak hem iOS hem de Android platformları için yerel (native) arayüze sahip mobil uygulamalar geliştirmemizi sağlayan açık kaynaklı bir framework'tür.

## React Native Nasıl Çalışır?
### Eski Mimari
React Native ile geliştirmiş bir uygulama Native uygulamaların aksine direk işletim sistemi tarafından değilde işletim sistemi üzerine inşa edilmiş Javascript motoru tarafından derlenir. Bu Javacript motoruna React Native Bridge diyoruz ve 3 ana bölümden oluşuyor.

![Resim 2](/gorsel/Resim2.png)

- [ ] **UI Thread** 
> Ekranda görüntülenecek bileşenlerin kontrolünü gerçekleştirir.
- [ ] **JS Thread** 
> Javascript ile geliştirilmiş tüm yapıların kontrolünü gerçekleştirir.
- [ ] **Native Thread** 
> Telefonun yerel bileşenlerine erişmek istediğimizdeki tüm sistemsel çağrıların kontrolünü gerçekleştirir.

### Yeni Mimari
Yeni mimari, Bridge tıkanıklığını ortadan kaldırmak için C++ tabanlı JSI (JavaScript Interface) üzerine inşa edilmiştir. Veriler JSON'a dönüştürülmeden, doğrudan bellekteki C++ nesne referanslarıyla iletilir.

- [ ] **JSI (JavaScript Interface)**
> Bridge yapısını tamamen kaldırır. JS katmanının C++ nesneleri üzerinden Native metotları doğrudan ve senkron olarak çağırmasını sağlar.

- [ ] **Fabric (Yeni Render Motoru)**
> Eski UI ve Shadow Tree yapısının yerini alan yeni UI motorudur. C++ seviyesinde çalıştığı için ekrandaki bileşen güncellemelerini çok daha hızlı ve senkron yapabilir (Uzun listelerdeki beyaz ekran kalma sorununu çözer).

- [ ] **TurboModules (Yeni Modül Yapısı)**
> Cihaz donanımlarına erişen modüllerin (kamera, konum vb.) çalışma biçimidir. Modüller uygulama ilk açıldığında değil, sadece ihtiyaç duyulduğunda (lazy-loading) hafızaya yüklenir. Bu da uygulamanın açılış süresini (TTI) belirgin şekilde hızlandırır.

- [ ] **CodeGen**
> JavaScript tarafındaki veri tipleri ile Native (C++/Swift/Java) taraftaki tipleri otomatik eşleştiren ve geliştirme anında tip hatalarını önleyen araçtır.

## React Native Proje Oluşturma Yaklaşımları

React Native ile bir proje geliştirmeye başlarken iki ana yaklaşım mevcuttur: **Expo** ve **React Native CLI**.

### Expo Go / EAS vs React Native CLI

| Özellik | Expo | React Native CLI |
| :--- | :--- | :--- |
| **Kurulum & Başlangıç** | Çok hızlı ve kolay. Xcode/Android Studio bağımlılığı olmadan başlanabilir. | Daha karmaşık. Android Studio, Xcode ve SDK konfigürasyonları gerektirir. |
| **Native Kod Müdahalesi** | `Prebuild` veya `Config Plugins` ile yönetilir, doğrudan Objective-C/Java yazma ihtiyacını minimuma indirir. | `android/` ve `ios/` klasörlerine tam erişim sağlar, doğrudan Native müdahale yapılabilir. |
| **Test Etme** | `Expo Go` mobil uygulaması ile QR kod taranarak fiziksel cihazda anında test edilebilir. | Simülatör/Ematör veya kablo ile cihaza build alma zorunluluğu vardır. |
| **Özel Native Kütüphaneler** | Expo ekosistemindeki zengin modüller ve Config Plugin destekli üçüncü taraf kütüphaneler kullanılır. | Tüm yerel C++/Java/Swift kütüphaneleri sorunsuz entegre edilebilir. |
| **Derleme (Build)** | EAS (Expo Application Services) ile bulut üzerinde derlenebilir (Mac olmadan iOS çıktısı alınabilir). | Yerel makinede derlenir (iOS çıktısı için Mac zorunludur). |

### Proje Oluşturma Adımları

#### 1. Expo Yapısı ile Proje Oluşturma
Expo, özellikle hızlı prototipleme ve kolay bakım gerektiren projelerde tercih edilen modern standarttır.

```bash
# Yeni bir Expo projesi oluşturma
npx create-expo-app MyProject

# Proje dizinine geçiş
cd MyProject

# Uygulamayı başlatma
npx expo start
```
#### 2. React Native CLI ile Proje Oluşturma
Tamamen özelleştirilebilir ve saf Native yapıya ihtiyaç duyulan büyük ölçekli projelerde tercih edilir.

```bash
# React Native CLI ile proje oluşturma
npx react-native@latest init MyProject

# iOS bağımlılıklarını yükleme (Sadece macOS için)
cd MyProject/ios && pod install && cd ..

# Uygulamayı çalıştırma
npx react-native run-android # Android için
npx react-native run-ios     # iOS için
```

## React Native Temelleri

### JSX (JavaScript Syntax Extension) 
React ve React Native ortamında UI bileşenlerini HTML benzeri bir sözdizimiyle yazmamızı sağlayan format yapısıdır.
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
1.	#### Functional Components
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

2.	#### Class Components
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
        <Text style={{color:"red"}}>just red</Text>
      </View>
    );
};

export default App;
```

> Bir bileşenin karmaşıklığı arttıkça, birkaç stili tek bir yerde tanımlamak için StyleSheet.create kullanmak genellikle daha temizdir.

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
React ortamında değeri değiştiğinde tanımlanan componenti tekrar render etmesini sağlayan değişkenlere state adı verilir.

#### Class Component State Kullanımı
> React.Component’ini extend ettiği zaman React.Component’nin constructor’ı state’i componentimize tanımlar ve varsayılan değer olarak null atar. Daha sonrasında kendi state değerlerimizi belirlemek için componentimizin constructor’ında veya direkt olarak sınıf içerisinde tanımlamalarımızı gerçekleştirebiliriz.
> Constructor içerisinde tanımlamış olduğumuz statelere erişmek için this ifadesini kullanırız.

```javascript
//State Tanımlama
constructor(props) {
   super(props);
   this.state = { myState: 'Merhaba React Native' };
}

//State değerini değiştirme
this.setState({myState: 'Merhaba Dünya'})
```

#### Function Component State Kullanımı
> Class componentde React.Component içerisinde state mekanizması hazır olan bir yapıdan bileşenimizi türetiyorken functional component de bunu useState Hook ile sağlayabiliyoruz. useState bir dizi şeklinde tanımlanır; iki parametre alır: ilk parametre değişkenin (state) kendisi, ikincisi değişiklikleri atamamızı sağlayan fonksiyondur.

```javascript
//State Tanımlama
const [myState, setMyState]=useState("Merhaba React Native");

//State değerini değiştirme
setMyState('Merhaba Dünya')
```

### Lifecycle
Her componentin bir yaşam süreci vardır. Doğar, yaşar ve ölür. Biz geliştirme sürecinde bu componentlerin yaşam evrelerini lifecycle ile yönetiyoruz.

![Resim 1](/gorsel/Resim1.png)

#### Class Component Lifecycle

React Hooks gelmeden önce Class component yapısında kullanılan üç aktif life-cycle method bulunmaktadır bunlar:

- `componentDidMount()` — Bileşen ekrana ilk render edildikten hemen sonra çalışır (API istekleri için idealdir).
- `componentDidUpdate()` — Props veya State değişip bileşen yeniden render edildikten sonra çalışır.
- `componentWillUnmount()` — Bileşen ekrandan/hafızadan kaldırılmadan hemen önce çalışır (Timer temizleme, event listener kaldırma için kullanılır).

#### Functional Component Hook Lifecycle

React Hooks ile birlikte dünyamıza giren useEffect bu yapıları tek bir method altında kullanmamıza olanak sağlıyor.

Bileşen başlangıçta bir kez render edildiğinde çalışır:

```javascript
useEffect (()=>{

},[])
```

Bileşen update edildiğinde (dependency değişince) çalışır:

```javascript
useEffect (()=>{

},[dependencies])
```

Bileşen yapıdan çıkarıldığında (silinmesi, gösterilmemesi) cleanup çalışır:

```javascript
useEffect (()=>{ 

return()=>{}
},[])
```

### State Yönetimi
Veriler prop'lar aracılığıyla en üst componentden bir alt componenete (yukarıdan aşağıya) aktarılır. Ancak bu tür bir kullanım büyük bir uygulama içindeki birçok componenet arası veri aktarımı işlemi için zor ve kullanışsız bir yöntem olacaktır. Context ve Redux vb. yöntemler componentlerin her seviyesinden açıkça bir prop geçirmek zorunda kalmadan bileşenler arasında bu gibi değerleri paylaşmanın bir yolunu sağlar.

![Resim 4](/gorsel/Resim4.png)

#### Context API
> React’ın kendi geleneksel context yapısını kullanarak global bir state yönetimi tasarlama yöntemidir. Global state değerleri çok fazla değişmeyecekse, birden fazla context yapısı kullanacaksak bu yöntemi tercih edebiliriz.

#### Redux
> Redux state bileşenlerini yönetmemizi sağlayan kütüphanedir. Global statelerimizde sık sık veri güncellemesi yapacaksak, birden fazla reducer'a ihtiyaç duyacaksak bu yöntemi tercih edebiliriz. Redux’ta veri aktarımı `Action`, `Reducer` ve `Store` ile gerçekleştirilir ve UI’a sunulur.

![Resim 5](/gorsel/Resim5.png)

- **Action:** Uygulama içerisinden store’a iletilen değişkenlerin bilgilerini tutar.
- **Reducer:** Action sonucunda uygulamanın var olan state’ini değiştirmesini sağlar. Uygulama değişikliğinin state’e aktarılması reducer tarafından olur.
- **Store:** Action ve reducer’ı bir araya getirip yapıyı bağlar. Uygulamanın state’ini tutar ve bazı metodlar ile bu state’e erişim yapılmasını sağlar.
- **Provider:** Store’un tüm uygulamaya etki etmesini sağlayan, uygulamanın etrafını sarmalayan bir yapıdır.

#### Redux Saga
> `Redux Saga` asenkron akışların okunmasını, yazılmasını ve test edilmesini kolaylaştırmak için kullanılan bir kütüphanedir. Bir Redux ara yazılımıdır; normal Redux eylemleriyle ana uygulamadan başlatılabilir, duraklatılabilir ve iptal edilebilir, tüm Redux uygulama durumuna erişebilir ve Redux eylemlerini de gönderebilir.

![Resim 7](/gorsel/Resim7.png)

### Memoization / Re-Render (Performans Optimizasyonu)
Bazen uygulamalarımızda fazla işlemci tüketen fonksiyonlar veya gereksiz re-render eden componentlerden kaynaklı performans sorunları yaşayabiliriz. Bu performans sorunlarını önlemek için Class componentler için `Pure Component` ve `shouldComponentUpdate`, Functional componentler için `useMemo` ve `useCallback` yöntemlerini kullanabiliriz.

#### `useMemo()`
> Fonksiyonlardaki fazla işlemci tüketen işlemler olduğu durumlarda fonksiyon her çağrıldığında bu işlemleri yapmak yerine fonksiyondan dönen son değeri hafızasında tutar. Son değeri (dependency array) referans alarak son değer değişmedikçe cache’deki değeri döndüren bir yöntemdir.

#### `useCallback()`
> Bir component her render edildiğinde component içerisindeki fonksiyonlar da tekrardan oluşturulur. Bu da büyük projelerde performans açısından kötü sonuçlar doğurabilir. Bu re-render maliyetini azaltmak için useCallback Hook’unu kullanırız.

#### `memo`
> Bir üst component render edildiğinde ona bağlı alt componentler de render olur. Alt componentlerde yansıyan herhangi bir değişiklik yok ise boşa render işlemi gerçekleşmiş olur. React.memo ile sarmaladığımız bir component kendisine gönderilen props değerlerini saklar. Bir sonraki render durumunda props değerleri bir öncekiyle karşılaştırılır; aynıysa component tekrar render edilmez.

Özetle `useMemo` fonksiyondan dönen değeri, `useCallback` dönen fonksiyonu ve `memo` ise componente gelen prop değerlerini hafızada tutarak gereksiz render işlemlerini önlememize yarıyor.

### Test İşlemleri
Projelerimizde kod yapıları genişledikçe beklenmeyen hatalar büyük sorunlara dönüşmektedir. Bir mobil uygulamayı kullanıma sunma süreci web uygulamalarına göre daha uzun bir süre almaktadır. Buglı bir mobil uygulamanın kullanıma sunulduktan sonra güncellemenin gönderilmesi zaman ve maliyet açısından sorun teşkil edecektir. Buda mobil uygulamaların kullanıma sunulmadan testlerinin yapılmasının önemini artırmaktadır. Testler ayrıca projeye yeni katılacak kişiler için kodların işlevselliği için belge görevi görecektir.

![Resim 6](/gorsel/Resim6.png)

> `Unit` testler bir uygulamada bulunan en küçük yapıların / birimlerin test edilmesidir. `Integration` testleri birbirinden farklı olan birimlerin bir araya gelerek oluşan yeni yapının doğru bir şekilde çalışıp çalışmadığının kontrol edilmesidir. `End to End` ve `UI` testleri son kullanıcı gibi davranarak uygulamaların tümünün kontrol edildiği testlerdir.

#### Unit Test
> Uygulamalarımızda test edebileceğimiz en küçük birimdir. Bir component üzerinde değişiklik yapılıp yapılmadığını, component üzerinden dönen propsların işlevselliğini, bir fonksiyonun istenen işlevselliği karşılayıp karşılamadığını ve componentlerin stil özelliklerini test edebiliriz.

##### Unit Test Araçları
> `Jest`: Facebook tarafından test için geliştirilmiş bir kütüphanedir. React ve React Native gibi frameworklerde kullanılabilir.
> `Testing Library`: React dokümanında testler için tavsiye edilen kütüphanedir. Testing Library, React Native için yardımcı fonksiyonlar sunar.

##### Snapshots Testi
> Bir componentin doğru bir şekilde render olup olmadığının ve component üzerinde değişiklik yapılıp yapılmadığının kontrol edildiği testtir.

```javascript
import React from 'react';
import {render} fom '@testing-library/react-native';
import Button from './Button';

test('should match with snapshot', ()=>{
const comp=render(<Button/>);
expect(comp).toMatchSnapshot();
})
```

##### Component Testi
> Component üzerinden dönen propsların işlevselliğinin kontrol edildiği testtir.

```javascript
import React from 'react';
import {render} fom '@testing-library/react-native';
import Button from './Button';

test('should render title correctly', ()=>{
const testTitle='test';
const comp=render(<Button title={testTitle} />);

const buttonText=comp.getByTestId('button-title').children[0];
expect(buttonText).toBe(testTitle);
})
```

##### Fonksiyon Testi
> Bir fonksiyonun istenilen işlevselliği karşılayıp karşılamadığının kontrol edildiği testtir.

```javascript
import React from 'react';
import {render, fireEvent} fom '@testing-library/react-native';
import Button from './Button';

test('should trigger onPress', ()=>{
const mockFunction=jest.fn();
const comp=render(<Button onClick={mockFunction} />);

const buttonTouchable=comp.getByTestId('button-touchable');
fireEvent(buttonTouchable,'press');

expect(mockFunction).toBeCalled();
})
```

##### Stil Testi
> Componentlerin stil özelliklerinin kontrol edildiği testtir.

```javascript
import React from 'react';
import {render} fom '@testing-library/react-native';
import Button from './Button';
import styles from './Button.style';

test('should render given theme style', ()=>{
const selectedTheme='primary'
const comp=render(<Button theme={selectedTheme} />);

const buttonStyle=comp.getByTestId('button-touchable').props.style;
expect(buttonStyle).toMatchObject(styles[selectedTheme].container);
})
```

#### Integration Testi
> Entegrasyon testi, farklı parçaların bir grup olarak test edildiği bir test türüdür.

```javascript
  const initialState = {
    todos: {
      todoList: ['buy groceries'],
    },
  };

  test('should display previous and new todos', async () => {
    const newTodoText = 'go running';
    const page = renderPage(<TodoList />, initialState);
    // GIVEN
    const TodoInput = page.getByPlaceholder(wording.todos.newTodo);
    const AddTodoButton = page.getByText(wording.todos.add);
    const FirstTodo = page.queryByText('buy groceries');
    expect(FirstTodo).toBeTruthy();
    // WHEN
    fireEvent.changeText(TodoInput, newTodoText);
    fireEvent.press(AddTodoButton);
    // THEN
    const NewTodo = await waitForElement(() => page.queryByText(newTodoText));
    expect(NewTodo).toBeTruthy();
  });
```
#### End to End Testi
> E2E testleri son kullanıcı gibi davranarak uygulamaların tümünün kontrol edildiği testlerdir. E2E testleri yapabileceğimiz çeşitli araçlar mevcuttur. Bunlardan en popüler olanı `Detox` kütüphanesidir. React Native uygulamaları için özel olarak tasarlanmıştır. Diğer popüler kütüphane `Appium`'dur.

```javascript
  test('should login successfully', async () => {
    await device.reloadReactNative();

    await element(by.id('email')).typeText('john@example.com');
    await element(by.id('password')).typeText('123456');
    await element(by.text('Login')).tap();

    await expect(element(by.text('Welcome'))).toBeVisible();
    await expect(element(by.id('email'))).toNotExist();
  });
```
![Resim 8](/gorsel/detoxtest.gif)


## React Native Yayınlama Süreçleri (Deployment)
Geliştirilen uygulamanın mağazalara (Google Play Store ve Apple App Store) gönderilme sürecidir.

### Android Yayınlama Süreci (Google Play Store)
Not: Google Play Console'a uygulama yüklemek için bir Google Play Developer hesabı (~$25 tek seferlik) gerekir. Keystore dosyasını kaybetmemeye dikkat edin; kaybedilirse uygulama güncellemesi yayınlanamaz.

- [ ] Keystore (İmza Anahtarı) Oluşturma: Uygulamanın size ait olduğunu doğrulamak için dijital bir imza anahtarı oluşturulur.
```bash
keytool -genkeypair -v -storetype PKCS12 -keystore my-upload-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000
```
- [ ] Gradle Yapılandırması: Oluşturulan .keystore dosyası android/app dizinine konur ve android/gradle.properties ile android/app/build.gradle dosyalarına anahtar bilgileri tanımlanır.
- [ ] App Icon ve Splash Screen: Hazırlanan ikon dosyaları ilgili yoğunluk klasörlerine elle konur.
  - Klasör: `android/app/src/main/res/`
  - `mipmap-mdpi`, `mipmap-hdpi`, `mipmap-xhdpi`, `mipmap-xxhdpi`, `mipmap-xxxhdpi` içine `ic_launcher.png` (ve yuvarlak ikon için `ic_launcher_round.png`) yerleştirilir.
  - Adaptive icon kullanılıyorsa `mipmap-anydpi-v26/ic_launcher.xml` ile birlikte `ic_launcher_foreground` / `ic_launcher_background` drawable’ları eklenir.
  - Splash screen: `drawable` / `values` altındaki splash kaynakları veya Android 12+ Splash Screen API / splash kütüphanesi ile ayarlanır.
- [ ] Sürüm Bilgisi: android/app/build.gradle içinde versionCode (her yüklemede artmalı) ve versionName güncellenir.
- [ ] Release Paket Oluşturma (AAB Formatı):
```bash
cd android
./gradlew bundleRelease
# Windows için: gradlew.bat bundleRelease
```
Çıktı: android/app/build/outputs/bundle/release/app-release.aab
- [ ] Google Play Console'a Yükleme: Oluşturulan .aab dosyası Play Console'a yüklenir.
- [ ] Mağaza Bilgileri ve Görseller: Kısa/uzun açıklama, gizlilik politikası URL'si, telefon/tablet ekran görüntüleri ve feature graphic (1024x500) doldurulur; Data safety formu tamamlanır.
- [ ] Dahili / Kapalı Test ve İnceleme: Uygulama önce Internal veya Closed testing ile test edilir, ardından Production incelemesine gönderilir.

### iOS Yayınlama Süreci (Apple App Store)
Not: iOS çıktısı alabilmek ve derlemek için bir macOS cihaza ve Apple Developer Program ($99/yıl) üyeliğine ihtiyaç vardır.

- [ ] Certificates & Provisioning Profiles: Apple Developer hesabında App ID tanımlanır, Distribution Certificate ve Provisioning Profile oluşturulur.
- [ ] App Icon ve Splash Screen: Hazırlanan ikon dosyaları ilgili asset klasörüne konur.
  - Klasör: `ios/<ProjeAdi>/Images.xcassets/AppIcon.appiconset/`
  - AppIcon setindeki boyut yuvalarına (20pt, 29pt, 40pt, 60pt, 1024pt vb.) uygun PNG’ler yerleştirilir; Xcode’da AppIcon alanına sürükleyerek de eklenebilir.
  - Splash / Launch Screen: `LaunchScreen.storyboard` veya ilgili launch image asset’leri ile ayarlanır.
- [ ] Sürüm Bilgisi: Xcode veya ios proje ayarlarında Version (CFBundleShortVersionString) ve Build (CFBundleVersion) güncellenir.
- [ ] Xcode Üzerinden Archive Alma:
  - [ ] Proje Xcode ile açılır (ios/MyProject.xcworkspace).
  - [ ] Hedef cihaz olarak Any iOS Device (arm64) seçilir.
  - [ ] Üst menüden Product > Archive adımı takip edilir.
- [ ] App Store Connect'e Yükleme: Organizer penceresinden Distribute App seçeneği ile uygulama App Store Connect'e gönderilir.
- [ ] Mağaza Bilgileri ve Görseller: Açıklama, gizlilik politikası URL'si, iPhone/iPad ekran görüntüleri ve Privacy Nutrition Labels doldurulur.
- [ ] TestFlight ve İnceleme: Uygulama önce TestFlight ile iç/dış testlere sunulabilir, ardından Apple incelemesine gönderilir.

### OTA (Over-The-Air) Güncellemeler
React Native'in sunduğu en büyük avantajlardan biri, Native kod değişikliği gerektirmeyen (sadece JS ve Asset değişiklikleri) güncellemeleri mağaza onayına sunmadan doğrudan kullanıcının cihazına aktarabilmesidir.
- [ ] Expo Updates (EAS Update): Expo projelerinde tek bir komutla yayın içi JavaScript paketini günceller.
```bash
eas update --branch production --message "Kritik bug düzeltildi"
```
- [ ] CodePush (Microsoft App Center / Appflow): React Native CLI projelerinde sıklıkla kullanılan canlı güncelleme servisidir.

⚠️ Önemli Not: Eğer yapılan değişiklik yeni bir Native kütüphane eklenmesini veya Swift/Java kodlarında değişiklik yapılmasını gerektiriyorsa OTA güncellemesi kullanılamaz; mağazalara yeni versiyon (AAB/IPA) çıkılması gerekir.

## Sık Kullanılan Komutlar (CLI / Expo)

Geliştirme sırasında paket yönetimi, ortam kontrolü, cache temizliği ve native derleme için sık kullanılan komutlardır. Aşağıda her komutun **ne işe yaradığı** ve **hangi yaklaşımda kullanıldığı** belirtilmiştir.

> **CLI** = React Native CLI (`android/` / `ios/` klasörleri projede hazır)  
> **Expo** = Expo / EAS tabanlı proje  
> **Her ikisi** = npm/yarn paket katmanı ortak olduğu için her iki yapıda da geçerli

### Paket Yönetimi

| Komut | Ne işe yarar? | Ne zaman gerekir? | CLI | Expo |
| :--- | :--- | :--- | :---: | :---: |
| `npm outdated` | Kurulu paketlerin güncel sürümden geride olup olmadığını listeler. | Bağımlılıkları denetlemek, güvenlik/uyumluluk kontrolü yapmak için. | ✅ | ✅ |
| `npm update paketAdi` | Belirtilen paketi `package.json` semver aralığı içinde günceller. | Küçük/patch güncellemeleri almak için. Major sürüm için genelde `npm install paketAdi@latest` tercih edilir. | ✅ | ✅ |
| `npm install` / `npm ci` | `package.json` / `package-lock.json`’a göre bağımlılıkları kurar. | Repo ilk açıldığında veya `node_modules` bozulduğunda. `ci` CI ortamında birebir kurulum içindir. | ✅ | ✅ |
| `npx expo install paketAdi` | Expo SDK ile uyumlu sürümü seçerek paket kurar. | Expo’da rastgele sürüm kurup SDK uyumsuzluğu yaşamamak için. | ❌ | ✅ |

```bash
npm outdated
npm update react-native-gesture-handler
# Expo'da uyumlu kurulum:
npx expo install react-native-gesture-handler
```

### Ortam ve Proje Sağlığı

| Komut | Ne işe yarar? | Ne zaman gerekir? | CLI | Expo |
| :--- | :--- | :--- | :---: | :---: |
| `npx react-native doctor` | Node, JDK, Android SDK, Xcode, adb vb. kurulumları kontrol eder; eksikleri gösterir. | İlk kurulumda veya “build almıyor” sorunlarında ortamı doğrulamak için. | ✅ | ⚠️ (kısmen; Expo’da asıl kontrol `npx expo-doctor`) |
| `npx expo-doctor` | Expo projesinin bağımlılık ve yapılandırma uyumunu kontrol eder. | Expo SDK yükseltmesi sonrası veya garip runtime hatalarında. | ❌ | ✅ |
| `npx expo start` | Expo geliştirme sunucusunu başlatır (Metro + QR). | Expo ile günlük geliştirme. | ❌ | ✅ |
| `npx react-native start` | Metro bundler’ı başlatır. | CLI projesinde JS paketini sunmak için. | ✅ | ⚠️ (Expo’da `expo start` tercih edilir) |
| `npx react-native run-android` / `run-ios` | Native uygulamayı derleyip cihaz/emülatöre yükler. | CLI’da uygulama + native katmanı birlikte çalıştırmak için. | ✅ | ⚠️ (prebuild sonrası veya dev client ile) |
| `npx expo run:android` / `run:ios` | Expo’da native derleme alıp cihazda çalıştırır (Dev Client / bare benzeri). | Expo Go yetmezse veya native modül testinde. | ❌ | ✅ |

```bash
npx react-native doctor
npx expo-doctor
```

### Cache Temizliği (Sık Karşılaşılan “eski kod geliyor” sorunları)

| Komut | Ne işe yarar? | Ne zaman gerekir? | CLI | Expo |
| :--- | :--- | :--- | :---: | :---: |
| `npm start -- --reset-cache` | Metro cache’ini sıfırlayarak bundler’ı başlatır. | Hâlâ eski bundle/cache’li kod göründüğünde, garip transform hatalarında. | ✅ | ⚠️ |
| `npx expo start -c` | Expo Metro cache’ini temizleyerek başlatır. | Expo’da cache kaynaklı hatalarda. | ❌ | ✅ |
| `watchman watch-del-all` | (varsa) Watchman dosya izleme cache’ini temizler. | Dosya değişikliklerinin algılanmadığı durumlarda. | ✅ | ✅ |
| `cd android && ./gradlew clean` | Android native derleme çıktılarını temizler. | Native bağımlılık/ikon/gradle değişikliği sonrası bozuk build’lerde. | ✅ | ⚠️ (`android/` varsa / prebuild sonrası) |

```bash
# CLI / genel Metro
npm start -- --reset-cache
# veya
npx react-native start --reset-cache

# Expo
npx expo start -c
```

### Android Gradle Derleme Komutları

Bu komutlar `android/` klasörü olan projelerde çalışır: **React Native CLI** ve **Expo prebuild / run** sonrası.

| Komut | Ne işe yarar? | Ne zaman gerekir? | CLI | Expo |
| :--- | :--- | :--- | :---: | :---: |
| `./gradlew assembleDebug` | Debug APK üretir (imza/yayın için değil, geliştirme/test için). | Hızlı native debug paketi almak, cihaza elle APK yüklemek için. | ✅ | ⚠️ (`android/` varsa) |
| `./gradlew assembleRelease` | Release APK üretir. | APK olarak dağıtım/test (Play Store artık AAB ister). | ✅ | ⚠️ |
| `./gradlew bundleRelease` | Release AAB üretir (Play Store yükleme formatı). | Mağazaya yayın paketini hazırlamak için. | ✅ | ⚠️ |
| `./gradlew clean` | Önceki derleme artığını siler. | Cache’li / bozuk native build sonrası temiz derleme için. | ✅ | ⚠️ |

```bash
cd android
./gradlew clean
./gradlew assembleDebug
./gradlew assembleRelease
./gradlew bundleRelease
# Windows:
gradlew.bat assembleDebug
```

> **Debug vs Release:** `assembleDebug` geliştirme imzası ve debug ayarlarıyla paketler; `assembleRelease` / `bundleRelease` yayın imzası (keystore) ve optimize edilmiş çıktı üretir. Play Store için tercih edilen çıktı **AAB** (`bundleRelease`)’dir.

### iOS (macOS) Karşılıkları

| Komut | Ne işe yarar? | CLI | Expo |
| :--- | :--- | :---: | :---: |
| `cd ios && pod install` | CocoaPods native bağımlılıklarını kurar/günceller. | ✅ | ⚠️ (`ios/` varsa) |
| `xcodebuild` / Xcode Archive | IPA / archive üretimi (mağaza yükleme öncesi). | ✅ | ⚠️ (veya `eas build`) |

### Expo’ya Özel Build / Yayın Komutları

| Komut | Ne işe yarar? | Ne zaman gerekir? |
| :--- | :--- | :--- |
| `eas build -p android` / `-p ios` | Bulutta native build alır (Mac olmadan iOS build mümkün). | Mağaza veya internal dağıtım paketi üretmek için. |
| `eas submit` | Üretilen build’i Play Console / App Store Connect’e gönderir. | Yayın yüklemesini otomatikleştirmek için. |
| `eas update` | OTA ile JS/asset güncellemesi yayınlar. | Native değişiklik yokken hızlı hotfix için. |

```bash
eas build -p android
eas build -p ios
eas submit -p android
eas update --branch production --message "Bug fix"
```

### Kısa Özet

- **Her iki yapıda da:** `npm outdated`, `npm update`, cache reset, (gerekirse) watchman temizliği.
- **Özellikle CLI:** `npx react-native doctor`, `run-android` / `run-ios`, `./gradlew assembleDebug|assembleRelease|bundleRelease`, `pod install`.
- **Özellikle Expo:** `npx expo-doctor`, `npx expo start -c`, `npx expo install`, `eas build` / `eas submit` / `eas update`.
- **Gradle komutları** yalnızca `android/` klasörü varken anlamlıdır; managed Expo Go akışında günlük geliştirmede gerekmez, prebuild veya EAS native build senaryosunda devreye girer.
## Proje Yükseltme (Upgrade)

React Native ve bağımlılıklar zamanla güncellenir. Güvenlik yamaları, yeni mimari (New Architecture), mağaza gereksinimleri (hedef SDK) ve kütüphane uyumu için periyodik yükseltme gerekir. **CLI** ve **Expo** yolları farklıdır.

### React Native CLI Yükseltme

CLI projelerinde sadece `package.json` sürümünü yükseltmek yetmez; `android/` ve `ios/` altındaki native şablon dosyaları da değişmiş olabilir. Bu farkları görmek için resmi araç:

[React Native Upgrade Helper](https://react-native-community.github.io/upgrade-helper/)

#### Upgrade Helper nasıl kullanılır?

1. Siteyi açın: [upgrade-helper](https://react-native-community.github.io/upgrade-helper/)
2. **App name** ve **App package** alanlarını projenize göre doldurun (diff’teki örnek isimlerin doğru üretilmesi için).
3. **Current version:** şu anki `react-native` sürümünü seçin (`package.json` → `"react-native"`).
4. **Target version:** yükselmek istediğiniz sürümü seçin.
5. **Show me how to upgrade!** butonuna tıklayın.
6. Araç, iki RN şablonu arasındaki dosya farklarını (eklenen / silinen / değişen satırlar) gösterir.
7. Listedeki her dosyayı kendi projenizle karşılaştırıp aynı değişiklikleri elle uygulayın (`android/`, `ios/`, kök config dosyaları vb.).

#### CLI yükseltme adımları (özet)

- [ ] Yeni bir git branch açın.
- [ ] Upgrade Helper’da current → target seçip diff’i inceleyin.
- [ ] JS bağımlılıklarını güncelleyin:

```bash
npm install react-native@<hedef-surum>
# veya
yarn add react-native@<hedef-surum>
```

- [ ] Upgrade Helper’da görünen native / config değişikliklerini tek tek uygulayın (`build.gradle`, `Podfile`, `AppDelegate`, `AndroidManifest.xml` vb.).
- [ ] iOS’ta pod’ları yenileyin:

```bash
cd ios
pod install
# sorun olursa:
pod deintegrate && pod install
cd ..
```

- [ ] Android’de temiz derleme alın:

```bash
cd android
./gradlew clean
cd ..
```

- [ ] Ortamı ve uygulamayı doğrulayın:

```bash
npx react-native doctor
npm start -- --reset-cache
npx react-native run-android
npx react-native run-ios
```

- [ ] Üçüncü taraf native kütüphanelerin hedef RN sürümüyle uyumunu kontrol edin; gerekirse onları da yükseltin (`npm outdated`).

> **Not:** Büyük sürüm atlamalarında (ör. 0.72 → 0.76) ara sürümlere basamak basamak çıkmak çoğu zaman daha güvenlidir. Helper’da her adım için ayrı diff alabilirsiniz.

### Expo Yükseltme

Expo’da asıl sürüm birimi **Expo SDK**’dır. SDK yükselince uyumlu `react-native`, `react` ve Expo modül sürümleri birlikte gelir. Managed / EAS akışında Upgrade Helper yerine Expo’nun kendi yükseltme yolu kullanılır.

#### Expo yükseltme adımları (özet)

- [ ] Mevcut SDK’yı öğrenin (`app.json` / `app.config.js` → `sdkVersion` veya `expo` paket sürümü).
- [ ] Hedef SDK’ya çıkın (örnek):

```bash
npx expo install expo@latest
# veya belirli SDK:
npx expo install expo@^52.0.0
```

- [ ] Expo’nun önerdiği bağımlılık sürümlerini hizalayın:

```bash
npx expo install --fix
```

- [ ] Uyumluluk kontrolü çalıştırın:

```bash
npx expo-doctor
```

- [ ] Cache temizleyip deneyin:

```bash
npx expo start -c
```

- [ ] Native klasör kullanıyorsanız (`android/` / `ios/` prebuild ile üretildiyse) temiz yeniden üretin:

```bash
npx expo prebuild --clean
# ardından
npx expo run:android
npx expo run:ios
```

- [ ] EAS kullanıyorsanız yeni SDK ile cloud build alın:

```bash
eas build -p android
eas build -p ios
```

> **Expo Go notu:** Telefonunuzdaki Expo Go uygulaması da hedef SDK’yı desteklemelidir. Desteklemiyorsa Development Build / `expo run:*` kullanın.

### CLI vs Expo — Ne zaman hangisi?

| Konu | React Native CLI | Expo |
| :--- | :--- | :--- |
| Ana araç | [Upgrade Helper](https://react-native-community.github.io/upgrade-helper/) + elle native diff | `npx expo install` / `expo install --fix` + `expo-doctor` |
| Ne değişir? | `react-native` + `android/` + `ios/` şablonları | Expo SDK + uyumlu RN/React + Expo modülleri |
| Native dosyalar | Diff’teki değişiklikler elle uygulanır | Çoğu zaman `prebuild --clean` veya EAS build ile yenilenir |
| Doğrulama | `react-native doctor`, `run-android` / `run-ios` | `expo-doctor`, `expo start -c`, `eas build` |

### Yükseltme sonrası kontrol listesi (ortak)

- [ ] Uygulama açılıyor mu? (debug)
- [ ] Kritik ekranlar / navigasyon / BLE-kamera vb. native özellikler çalışıyor mu?
- [ ] Release / AAB veya EAS production build sorunsuz mu?
- [ ] Kırılan peer dependency uyarısı kaldı mı? (`npm outdated`, `expo-doctor`)
- [ ] Mağaza hedef SDK / Privacy / Data safety gereksinimleri hâlâ karşılanıyor mu?
