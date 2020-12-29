# Erişim Denetimi

Nesne yönelimli programlamanın 4 temel kavramından biri **kapsüllemedir (encapsulation).** Bu kavram basitçe, sınıfın içine yazdığımız alanları ve metotları gizleyebileceğimizi ifade eder. Bu gizleme farklı seviyelerde olabilir. Alanları ve metotları gizleyebilmek için **erişim belirteçleri**ni **(access modifiers)** kullanırız.

## Erişim Belirteçleri

Java’da 4 adet erişim belirteci vardır:

- **public**: Bu erişim belirteciyle belirtilen bir alana veya metoda her yerden erişilebilir. **public** deyimini kullanır. Gizlilik seviyesi en düşük olan erişim belirtecidir.
- **default:** Yalnızca aynı paket içinden erişilebilir. Bu belirteç _default_ olarak isimlendirilmesine rağmen, herhangi bir deyim yazılmaz.
- **protected:** Yalnızca aynı paket içinden veya alt sınıflardan erişilebilir. **protected** deyimini kullanır.
- **private:** Yalnızca aynı sınıf içinden erişilebilir. private deyimini kullanır. Gizlilik seviyesi en yüksek olan erişim belirtecidir.

## Neden Erişim Belirteçleri Gereklidir ?

- Hassas verilerin saklanması sağlanır, erişim kısıtlanır ([Principle Of Least Privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege) - PoLP yaklaşımı)
- Sınıfı kullanacak olan geliştiricilerin hangi üyelere erişebileceği belirlenir.
- Verilerin tutarlılığı sağlanır.

Aşağıdaki örnekleri inceleyelim:

```java
package package1;

class Box
{
	public int width;
	public int height;
	public int depth;
}
```

```java
package package2;

class Main
{
	public static void main(String[] args)
	{
		Box box = new Box();
		box.width = 100;
	}
}
```

Yukarıdaki örnekte _Box_ ve _Main_ sınıfları farklı paketler içindedir. Buna rağmen, _Box_ sınıfının alanları **public** olarak belirtildiği için, farklı pakette olmasına rağmen _Main_ sınıfından erişilebilir.

```java
package package1;

class Box
{
	int width;
	int height;
	int depth;
}
```

```java
package package2;

class Main
{
	public static void main(String[] args)
	{
        Box box = new Box();
	    box.width = 100; // Bu satır hataya sebep olur
	}
}
```

Yukarıdaki örnekte Box sınıfının alanlarına erişim **default** olarak belirlenmiştir, yalnızca **package1** paketinin içinden erişilebilir. Bu yüzden, _Main_ sınıfı **package2** paketi içinde olduğu için _Box_ sınıfının alanlarına erişmeye çalışıldığında hata fırlatılır.

```java
package package1;

class Box
{
	private int width;
	private int height;
	private int depth;
}
```

```java
package package1;

class Main
{
	public static void main(String[] args)
    {
		Box box = new Box();
		box.width = 100; // Bu satır hataya sebep olur
	}
}
```

Yukarıdaki örnekte _Box_ ve _Main_ sınıfları aynı paket içinde olmalarına rağmen, _Main_ sınıfından _Box_ sınıfının alanlarına erişilemez. _Box_ sınıfının alanları private olarak belirtildiği için yalnızca aynı sınıf içinden erişilebilir.

Yukarıdaki örnekler ile public, protected, private ve default (package-private) erişim belirleyicileri hakkında biraz daha bilgi sahibi olduktan sonra kafamızda takılan soru işareti varsa ya da sözel olarak karışık geldiyse aşağıdaki tablo kafanızdaki soru işaretlerini giderecektir. (Tablodaki kutucuklardaki X işareti olan kısımlar erişilebilir olduğunu göstermektedir. Boş olan kısımlar ise erişilemez olduğunu göstermektedir.)

| Erişi Düzenleyicisi              | public | protected | private | default |
| :------------------------------- | :----: | :-------: | :-----: | :-----: |
| Aynı sınıf                       |   X    |     X     |    X    |    X    |
| Aynı paketteki alt sınıflardan   |   X    |     X     |         |    X    |
| Aynı paket - Alt Sınıf Yok       |   X    |     X     |         |    X    |
| Farklı paketteki alt sınıflardan |   X    |     X     |         |         |
| Farklı paket - Alt Sınıf Yok     |   X    |           |         |         |

