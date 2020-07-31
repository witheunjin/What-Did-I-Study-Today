# 2020.07.31

## ViewModel

### ViewModel 클래스

- 수명 주기를 고려하여 UI관련 데이터 저장 혹은 관리

- 화면 회전처럼 구성변경 시에도 데이터를 유지할 수 있게 함

- ViewModel을 사용하므로써 해결되는 문제들

  - 시스템에서 UI controller를 제거하거나 다시 만들 경우, controller에 저장되어 있던 모든 UI 관련 데이터가 소실된다. 구성 변경을 위해 액티비티가 재생성되는 경우 사용자 목록을 다시 가져와야 한다. 데이터가 단순한 경우에는 `onSaveInstanceState()`메서드를 사용하여 `onCreate()` 번들에서 복원할 수 있지만, 소량의 데이터만 해당한다. 
  - UI controller는 비동기 호출을 관리하는데 여기에는 많은 유지보수가 필요하고, 컴포넌트 변경 시 개체가 재생성되면 개체가 이미 실행된 호출을 다시 해야하는 일이 생기는데, 여기서 리소스의 낭비가 발생한다.
  - UI controller에 데이터 로드를 담당하면 클래스가 팽창되고, 테스트가 어렵다. 

- Ui controller logic 으로부터 view data 소유권을 분리하는 방법이 바로 ViewModel이다. 

- ViewModel 객체는 컴포넌트가 변경되는 동안, 자동으로 보관된다. 따라서 ViewModel이 가지고 있는 데이터는 다음 Activity나 fragment instance에서 즉시 사용할 수 있다. 

- 다음은 사용자 목록이라는 데이터를 activity/fragment 대신 ViewModel에 할당하는 코드이다.

- ```kotlin
      class MyViewModel : ViewModel() {
          private val users: MutableLiveData<List<User>> by lazy {
              MutableLiveData().also {
                  loadUsers()
              }
          }
  
          fun getUsers(): LiveData<List<User>> {
              return users
          }
  
          private fun loadUsers() {
              // Do an asynchronous operation to fetch users.
          }
      }
      
  ```

- 다음은 activity에서 목록(데이터)에 접근하는 코드이다. 

- ```kotlin
      class MyActivity : AppCompatActivity() {
  
          override fun onCreate(savedInstanceState: Bundle?) {
              // Create a ViewModel the first time the system calls an activity's onCreate() method.
              // Re-created activities receive the same MyViewModel instance created by the first activity.
  
              // Use the 'by viewModels()' Kotlin property delegate
              // from the activity-ktx artifact
              val model: MyViewModel by viewModels()
              model.getUsers().observe(this, Observer<List<User>>{ users ->
                  // update UI
              })
          }
      }
      
  ```

