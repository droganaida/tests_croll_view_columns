# Unity3d UI (ScrollView Adapter): 3 колонки

## Дополнение к уроку от #BlondieCode Unity3d UI (ScrollView Adapter)

Вот, что должно получиться в результате (не очень красиво, зато прочно =D)

[!ScrollView Adapter 3 колонки](https://github.com/droganaida/tests_croll_view_columns/blob/master/Screens/usc-1.jpg)

Нужно изменить существующий prefab для элемента списка так, чтобы в нем появилось 3 колонки (или любое другое количество текстовых полей, картинок и кнопок).
Объединяем 3 компонента UI->Text в компоненте UI->Image.

[!ScrollView Adapter 3 колонки prefab](https://github.com/droganaida/tests_croll_view_columns/blob/master/Screens/usc-2.jpg)

Отправляем новый шаблон в скрипт. Теперь все айтемы скроллера будут иметь по три текстовых поля.

[!ScrollView Adapter 3 колонки script variable](https://github.com/droganaida/tests_croll_view_columns/blob/master/Screens/usc-3.jpg)

Логика заполнения списка здесь:
[ScrollViewAdapter.cs](https://github.com/droganaida/tests_croll_view_columns/blob/master/Assets/Scripts/ScrollViewAdapter.cs)
В скрипте изменяем модель для айтема так, чтобы количество полей совпадало с количеством колонок и типом данных (в каждой из них будет заголовок, описание, цена или картинка).
В нашем случае это три строковых поля.
```
public class TestItemModel
    {
        public string title;
		public string description;
		public string price;
    }
```

В графическом представлении айтема назначаем элементы под вывод полей. Теперь это 3 компонента Text из новых полей префаба.
```
public class TestItemView
    {
        public Text titleText;
		public Text descriptionText;
		public Text priceText;

        public TestItemView (Transform rootView)
        {
            titleText = rootView.Find("TitleText").GetComponent<Text>();
			descriptionText = rootView.Find("DescriptionText").GetComponent<Text>();
			priceText = rootView.Find("PriceText").GetComponent<Text>();
        }
    }
```

Расфасовываем значения строковых полей по компонентам:
```
IEnumerator GetItems (int count, System.Action<TestItemModel[]> callback)
    {
        yield return new WaitForSeconds(1f);
        var results = new TestItemModel[count];
        for (int i = 0; i < count; i++)
        {
            results[i] = new TestItemModel();
            results[i].title = "Item " + i;
            results[i].description = "Blabla " + i;
			results[i].price = "$ " + i;
        }

        callback(results);
    }
```
Готово!

[![Урок на YouTube #BlondieCode](http://img.youtube.com/vi/k-ajG_jmmtI/0.jpg)](http://www.youtube.com/watch?v=k-ajG_jmmtI)
