# 2020.07.24

**📚공부한 거 List**📚

- 안드로이드 - bottom navigation with fragment 디렉터리 구조 변경 & fragment 내용 채우기
- 안드로이드 - recyclerview 코드리뷰반영

----

## Bottom Navigation Activity

### 1. 변경 후:실행화면

| Home | Dashboard | Notifications|
|:-:|:-:|:-:|
|![image](https://user-images.githubusercontent.com/50702052/88293254-bad98600-cd35-11ea-98cb-3b67745e7f0c.png)|![image](https://user-images.githubusercontent.com/50702052/88293393-e9576100-cd35-11ea-824a-f2ab63d0f14f.png)|![image](https://user-images.githubusercontent.com/50702052/88293419-f1170580-cd35-11ea-9b0c-9cb4d3190f7a.png)|

### 2. 변경 후:디렉터리 구조

#### app/main/java/com.example.[APPNAME]

```
|_MainActivity.kt
|_/ui
   |/birthday
     |__BirthDayFragment.kt
     |__BirthDayViewModel.kt
   |/name
     |__NameFragment.kt
     |__NameViewModel.kt
   |_/school
     |__SchoolFragment.kt
     |__SchoolViewModel.kt
```

#### app/main/res

```
|_/drawable
   |__ic_dashboard_black_24dp.xml
   |__ic_home_black_24dp.xml
   |__ic_launcher_background.xml
   |__ic_notifications_black_24dp.xml
|_/drawable-v24*
|_/layout
   |__activity_main.xml
   |__fragment_birthday.xml
   |__fragment_name.xml
   |__fragment_school.xml
|_/menu
   |__bottom_nav_menu.xml
|_/navigation
   |__mobile_navigation.xml
|_/values
   |__colors.xml
   |__dimens.xml
   |__strings.xml
   |__styles.xml
```

_____

## recyclerview 코드리뷰반영
#### 1. DataType는 RecyclerView.Adapter<T>가 아닌 상속받는 adapter타입으로 설정
```kotlin
//이전 코드
private lateinit var viewAdapter: RecyclerView.Adapter<*>
//리뷰 반영 후 코드
private lateinit var viewAdpater: RecyclerView.Adpater<MyAdapter.ViewHolder>
```

#### 2. `findViewByID`보다 KTX(kotlin extension)을 사용

```kotlin
//이전 코드
recyclerview = findViewById<RecyclerView>(R.id.recyclerView).apply {...}
//리뷰 반영 후 코드
recyclerView.apply {...}
```

#### 3. `shuffle`을 adapter에서 하는 것보다 MainActivity에서 `onScrollAdpater`로 하는 게 메모리관점에서 더 좋다. 

adapter에서 shuffle을 하면 onBindViewHolder에서 notifyDatasetChanged를 호출하게 되어 뷰 생성을 자주 하기 때문.

```kotlin
//이전 코드(MyAdapter.kt)
 override fun onBindViewHolder(holder: ViewHolder, position: Int) {
        if(position == dataSet.size-1) {
        dataSet.shuffle()
        }
        ...
}
//리뷰 반영 후 코드
//추가 질문 답변 대기 중
```