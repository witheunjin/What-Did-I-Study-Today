# 2020.07.23

**📚공부한 거 List**📚

- 안드로이드 - bottom navigation with fragment 코드 분석

----

## Bottom Navigation Activity

android studio에서 New > Activity > Bottom Navigation Activity를 클릭하면 자동으로 파일들과 폴더들이 생성된다. 
### 1. 초기:실행화면

| Home | Dashboard | Notifications|
|:-:|:-:|:-:|
|![image](https://user-images.githubusercontent.com/50702052/88293254-bad98600-cd35-11ea-98cb-3b67745e7f0c.png)|![image](https://user-images.githubusercontent.com/50702052/88293393-e9576100-cd35-11ea-824a-f2ab63d0f14f.png)|![image](https://user-images.githubusercontent.com/50702052/88293419-f1170580-cd35-11ea-9b0c-9cb4d3190f7a.png)|

### 2. 초기:디렉터리 구조

#### app/main/java/com.example.[APPNAME]

```
|_MainActivity.kt
|_/ui
   |/dashboard
     |__DashBoardFragment.kt
     |__DashBoardViewModel.kt
   |/home
     |__HomeFragment.kt
     |__HomeViewModel.kt
   |_/notifications
     |__NotificationsFragment.kt
     |__NotificationsViewModel.kt
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
   |__fragment_dashboard.xml
   |__fragment_home.xml
   |__fragment_notifications.xml
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

## Fragment

[Android Developer:Fragment 설명 바로가기](https://developer.android.com/guide/components/fragments)

- 여러 개의 프래그먼트를 하나의 액티비티에 결합하여 창이 여러 개인 UI를 빌드할 수 있으며, 하나의 프래그먼트를 여러 액티비티에서 재사용할 수 있습니다.
- 프래그먼트는 항상 액티비티 내에서 호스팅되어야 하며 해당 프래그먼트의 수명 주기는 호스트 액티비티의 수명 주기에 직접적으로 영향을 받습니다.

#### LifeCycle

`onCreate()` : 프래그먼트를 생성할 때 호출된다.  프래그먼트가 일시정지되거나 중단되었다가 재개되었을 때 유지하고자 하는 것을 초기화하는 공간임.

`onCreateView()` : 시스템은 프래그먼트가 자신의 사용자 인터페이스를 처음으로 그릴 시간이 되면 이것을 호출합니다. 프래그먼트에 맞는 UI를 그리려면 메서드에서 `View`를 반환해야 합니다. 이 메서드는 프래그먼트 레이아웃의 루트입니다. 프래그먼트가 UI를 제공하지 않는 경우 null을 반환하면 됩니다.

`onPause()` : 시스템이 이 메서드를 호출하는 것은 사용자가 프래그먼트를 떠난다는 것을 나타내는 첫 번째 신호입니다(다만 항상 프래그먼트가 소멸 중이라는 것을 의미하지는 않습니다). 일반적으로 여기에서 현재 사용자 세션을 넘어서 지속되어야 하는 변경 사항을 커밋합니다(사용자가 돌아오지 않을 수 있기 때문입니다).

## ViewModel

[Android Developers:ViewModel 설명 바로가기](https://developer.android.com/reference/android/arch/lifecycle/ViewModel)

[Medium_ViewModels : A Simple Example 글 바로가기](https://medium.com/androiddevelopers/viewmodels-a-simple-example-ed5ac416317e)

- ViewModel은 UI와 관련된 데이터(=Activity나 Fragment의 데이터)를 생명주기동안 유지하고 관리하기 위해 고안된 것이다. 
- ViewModel을 사용하는 방법은 다음과 같다. 
  1. ViewMode을 상속하는 클래스를 만들어서 UI 컨트롤러의 데이터를 분리시킨다. 
  2. ViewModel과 UI controller의 데이터 소통을 구현한다.  
  3. UI controller에서 ViewModel을 사용한다. 

----

