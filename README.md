# React Native Türkçe Notlar

<!--ts-->
- [Mobil Programlama Nedir?](#mobil-programlama-nedir)
- [Mobil Uygulama Geliştirmek için Hangi Seçenekler vardır?](#mobil-uygulama-geliştirmek-için-hangi-seçenekler-vardır)
- [React Native Nedir?](#react-native-nedir)
- [React Native Nasıl Çalışır?](#react-native-nasıl-çalışır)
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
		- [``useMemo()``](#usememo)
		- [``useCallback()``](#usecallback)
		- [``memo``](#memo)
	- [Test İşlemleri](#test-i̇şlemleri)
		- [Unit Test](#unit-test)
			- [Unit Test Araçları](#unit-test-araçları)
			- [Snapshots Testi](#snapshots-testi)
			- [Component Testi](#component-testi)
			- [Fonksiyon Testi](#fonksiyon-testi)
			- [Stil Testi](#stil-testi)
		- [Integration Testi](#integration-testi)
		- [End to End Testi](#end-to-end-testi)

<!--te-->

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

1. #### Class Component Lifecycle

React Hooks gelmeden önce Class component yapısında kullanılan üç aktif life-cycle method bulunmaktadır bunlar;
- `componentDidMount()`
> Bileşen başlangıçta bir kez render edildiğinde çalışır.
-  `componentDidUpdate()`
> Bileşen update edildiğinde ait olduğu bileşen render edilir ve yenilenir.
-  `componentWillUnmount()`
> Bileşen yapıdan çıkarıldığında (silinmesi,gösterilmemesi) gibi durumlarda kullanılır .

2. #### Functional Component Hook Lifecycle

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

1. #### Context API
> React’ın kendi geleneksel context yapısını kullanarak global bir state yönetimi tasarlamaya yöntemidir. Global state değerleri çok fazla değişmeyecekse, birden fazla context yapısı kullanacaksak bu yöntemi tercih edebiliriz.

2. #### Redux
> Redux state bileşenlerini yönetmemizi sağlayan kütüphanedir. Gloal statelerimizde sık sık veri güncellemesi yapacaksak, birden fazla reducer'a ihtiyaç duyacaksak bu yöntemi tercih edebiliriz. Redux’ta veri aktarımı ``Action``, ``Reducer`` ve ``Store`` gerçekleştirilir ve UI’a sunulur.

![Resim 5](/gorsel/Resim5.png)

* ``Action``
Uygulama içerisinden store’a iletilen değişkenlerin bilgilerini tutar.

* ``Reducer``
Reducerlar, action sonucunda uygulamanın var olan state’i değiştirmesini sağlar. Uygulama değişikliğinin state’e aktarılması ise reducer tarafından olur.

* ``Store``
Store işlemi, action ve reducerı bir araya getirip yapıyı bağlar. Uygulamanın state’ini tutar ve bazı metodlar ile bu state’ erişim yapılmasını sağlar.

* ``Provider``
Store’un tüm uygulamaya etki etmesini sağlayan, uygulamanın etrafını sarmalayan bir yapıdır.

3. #### Redux Saga
> ``Redux saga`` asenkron akışların okunmasını, yazılmasını ve test edilmesini kolaylaştırmak için kullanılan bir kütüphanedir. Bir Redux ara yazılımıdır, yani bu iş parçacığı normal Redux eylemleriyle ana uygulamadan başlatılabilir, duraklatılabilir ve iptal edilebilir, tüm Redux uygulama durumuna erişebilir ve Redux eylemlerini de gönderebilir.

![Resim 7](/gorsel/Resim7.png)

### Memoization / Re-Render (Performans Optimizasyonu)
Bazen uygulamalarımızda fazla işlemci tüketen fonksiyonlar veya gereksiz re-render eden componentlerden kaynaklı performans sorunları yaşayabiliriz. Bu performans sorunlarını önlemek için Class componentler için ``Pure Component`` ve ``shouldComponentUpdate``, Functional componentler için ``useMome`` ve ``useCallback`` yöntemlerini kullanabiliriz.

* #### ``useMemo()``
> Fonksiyonlardaki fazla işlemci tüketen işlemler olduğu durumlarda fonksiyon her çağrıldığında bu işlemleri yapmak yerine fonksiyondan dönen son değeri afızasında tutar. Son değeri (dependency array) referans alarak son değer değişmedikçe cache deki değeri döndüren bir yöntemdir.


* #### ``useCallback()``
> Bir component her render edildiğinde component içerisindeki fonksiyonlarda da tekrardan oluşturulur. Bu da büyük projelerde component içerisindeki fonksiyonların tekrar tekar oluşturacağı için performans açısından kötü sonuçlar doğuracaktır. Bu re-render işlemini önlemek için useCallBack Hook'unu kullanıyoruz.

* #### ``memo``
> Bir üst component render edildiğinde ona bağlı alt componentlerde render olur. Alt componentlerde yansıyan herhangi bir değişlik yok ise boşa render işlemi gerçekleşmiş olur. React.memo ile sarmaladığımı bir component kendisine gönderilen props değerlerini saklar ve kaydeder. Bir sonraki render durumunda bu component’e gönderilen props değerleri,  bir önceki render edildiğindeki props değerleri ile karşılaştırır. Eğer props değerleri aynı ise componenti tekrar render etmez.

Özetle ``useMemo`` fonksiyondan dönen değeri, ``useCallback`` dönen fonksiyonu ve ``memo`` ise componentten dönen prop değerlerini hafızada tutarak gereksiz render işlemlerini önlememize yarıyor.

### Test İşlemleri
Projelerimizde kod yapıları genişledikçe beklenmeyen hatalar büyük sorunlara dönüşmektedir. Bir mobil uygulamayı kullanıma sunma süreci web uygulamalarına göre daha uzun bir süre almaktadır. Buglı bir mobil uygulamanın kullanıma sunulduktan sonra güncellemenin gönderilmesi zaman ve maliyet açısından sorun teşkil edecektir. Buda mobil uygulamaların kullanıma sunulmadan testlerinin yapılmasının önemini artırmaktadır. Testler ayrıca projeye yeni katılacak kişiler için kodların işlevselliği için belge görevi görecektir.

![Resim 6](/gorsel/Resim6.png)

> ``Unit`` testler bir uygulamada bulunan en küçük yapıların birimlerin test edilmesidir. ``Integration`` testleri birbirinden farklı olan birimlerin bir araya gelerek oluşan yeni yapının doğru bir şekilde çalışıp çalışmadığının kontrol edilmesidir. ``End to End`` ve ``UI`` testleri son kullanıcı gibi davranarak uygulamaların tümünün kontrol edildiği testlerdir.

1. #### Unit Test
> Uygulamalarımızda test edebileceğimiz en küçük birimdir. Bir component üzerinde değişiklik yapılıp yapılmadığını, component üzerinden dönen propsların işlevselliğini, bir fonksiyonun istenen işlevselliği karşılayıp karşılamadığını ve componentlerin stil özelliklerini test edebiliriz.

* ##### Unit Test Araçları
> ``Jest``: Facebook tarafından test için geliştirilmiş bir kütüphanedir. React ve React-Native gibi frameworklerde kullanabilmekteyiz. </br>
``Testing Library``: React dokümanında testler için tavsiye edilen kütüphanedir. Testing library React-Native için yardımcı fonksiyonlar sunar.


* ##### Snapshots Testi
> Bir component in doğru bir şekilde render olup olmadığının ve component üzerinde değişiklik yapılıp yapılmadığının kontrol edildiği testtir.
```javascript
import React from 'react';
import {render} fom '@testing-library/react-native';
import Button from './Button';

test('should match with snapshot', ()=>{
const comp=render(<Button/>);
expect(comp).toMatchSnapshot();
})
```
* ##### Component Testi
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
* ##### Fonksiyon Testi
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
* ##### Stil Testi
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
2. #### Integration Testi
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
3. #### End to End Testi
> E2E testleri son kullanıcı gibi davranarak uygulamaların tümünün kontrol edildiği testlerdir. E2E testleri yapabileceğimiz çeşitli araçlar mevcuttur. Bunlardan en popüler olanı ``Detox`` kütüphanesidir. React Native uygulamaları için özel olarak tasarlanmışır. Diğer popüler kütüphane ``Appium``'dur.

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
