# JohnnyFiveCodeStyle


# 1. Project guidelines

## 1.2 File naming

#### Class files

Classes' names that extend an Android component, should end with the name of the component.  
`SignInActivity`, `SignInFragment`, `ImageUploadService`, `ExitDialogFragment`.

#### Drawable files

Naming conventions for drawables:


| Asset Type   | Prefix            |		Example          |
|--------------| ------------------|-----------------------------|
| Button       | `btn_`	           | `btn_send_pressed.9.png`    |
| Divider      | `divider_`        | `divider_horizontal.9.png`  |
| Icon         | `ic_`	           | `ic_star.png`               |
| Tabs         | `tab_`            | `tab_pressed.9.png`         |
| Background   | `background_`     | `background_top_banner.xml` |

#### Layout files

Layout files should match the name of the Android components that they are intended for but moving the top level component name to the beginning.

| Component        | Class Name             | Layout Name                   |
| ---------------- | ---------------------- | ----------------------------- |
| Activity         | `UserProfileActivity`  | `activity_user_profile.xml`   |
| Fragment         | `SignUpFragment`       | `fragment_sign_up.xml`        |
| Dialog           | `ChangePasswordDialog` | `dialog_change_password.xml`  |
| RecyclerView item| ---                    | `list_item_address.xml`       |


#### Values files

Resource files in the values folder should be __plural__, e.g. `strings.xml`, `styles.xml`, `colors.xml`, `dimens.xml`, `attrs.xml`

Some additional files should be added to default set:  
`text_appearances.xml` - file with text styles.  
`colors_text.xml` - file with text colors (optional, if color set is too large).  
`dimens_text_sizes.xml` - file with text sizes (optional, if all text sizes covered in `text_appearances.xml`).  
`dimens_widths_heights.xml` - file with widths and heights.

# 2 Code guidelines

## 2.2 Java style rules

### 2.2.1 Naming

* If interface and class names are the same, use **Impl** postfix.  

| Interface      | Class          |
| -------------- | -------------- |
| `UserRepository` | `UserRepositoryImpl` |

* **No “m” or "s" letter in the name of a class member !**    
Let [this](https://stackoverflow.com/questions/2092098/why-do-most-fields-class-members-in-android-tutorial-start-with-m) relics of the past die peacfully in an endless jungle of the legacy code. 

* Do not shorten variables names.  
Use full and identical to class (or at least meaningful) name sequence. Prefer readability over conciseness.

| Good                                      | Bad            		 |
| ----------------------------------------- | -------------------------- |
| `SimpleDateFormatter simpleDateFormatter` | `SimpleDateFormatter sdf`  |
| `SimpleDateFormatter simpleDateFormatter` | `SimpleDateFormatter formatter`  |
| `Boolean isValid`  			    | `Boolean b`  		 |
		
* Name booleans according to rules of english language.

`Boolean shouldShow;`  
`Boolean hasDate;`  
`hasDate isValid;`  

* Treat acronyms as words.

| Good           | Bad            |
| -------------- | -------------- |
| `XmlHttpRequest` | `XMLHTTPRequest` |
| `getCustomerId`  | `getCustomerID`  |
| `String url`     | `String URL`     |
| `long id`        | `long ID`        |


### 2.2.5 Brace style

Braces go on the same line as the code before them.
Always use braces even if statement has one line. It make code more readable and consistent.

```java
class MyClass {
    int func() {
        if (something) {
            // ...
        } else if (somethingElse) {
            // ...
        } else {
            print("Hello");
        }
    }
}
```

### 2.2.10 Class member ordering

1. Constants 
2. Fields (initialized in constructor)
3. Local variables
4. View fields
5. getInstance()/newInstance() methods (if singleton)
6. Constructors
7. Lifecycle methods (in natural order)
8. Callbacks/anonymous classes
9. Public methods
10. Internal logic (private/protected methods)
11. Inner classes/interfaces (try to avoid inner classes if possible)

Each member groups should have a top indented of **one line** except for indent between fields and methods: it should be **two lines**.

Example:

```java
public class MainActivity extends BaseActivity {
    
    public static final String KEY_USER_ID = "KEY_USER_ID";

    public final int invalidId = -1;

    private Adapter adapter;
    private Service service;

    private ScrollView scrollView;
    private TextView tvTitle;


    //region ===================== Lifecycle ======================

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
    }
    
    @Override
    public void onDestroy() {
        super.onDestroy();
    }
    
    //endregion

    //region ===================== Callbacks ======================

    @Override
    public void onBackPressed() {
        super.onBackPressed();
    }
    
    private View.OnClickListener btnOkClickListener = v -> {};

    private View.OnClickListener btnCancelClickListener = v -> {};

    //endregion

    //region ===================== Internal ======================

    private void initUI() {
    }

    //endregion
}
```

### 2.2.11 Regions
//todo

### 2.2.11 Parameter ordering in methods

When programming for Android, it is quite common to define methods that take a `Context`. If you are writing a method like this, then the __Context__ must be the __first__ parameter.

The opposite case are __callback__ interfaces that should always be the __last__ parameter.

Examples:

```java
public User loadUser(Context context, int userId);

public User loadUser(Context context, int userId, OnUserLoadedCallback onUserLoadedCallback);
```

### 2.2.13 Сonstants-keys

Many elements of the Android SDK such as `SharedPreferences`, `Bundle`, or `Intent` use a key-value pair approach.
When using one of these components, you can simply name them as `KEY_`

```java
static final String KEY_EMAIL = "KEY_EMAIL"
static final String KEY_EMAIL = "KEY_AGE"
```
If class has a lot of keys, you may (__optionally__) use these prefixes.

| Element            | Field Name Prefix |
| -----------------  | ----------------- |
| SharedPreferences  | `PREF_`             |
| Bundle             | `BUNDLE_`           |
| Fragment Arguments | `ARGUMENT_`         |
| Intent Extra       | `EXTRA_`            |
| Intent Action      | `ACTION_`           |


Example:

```java
static final String PREF_EMAIL = "PREF_EMAIL";
static final String BUNDLE_AGE = "BUNDLE_AGE";
static final String ARGUMENT_USER_ID = "ARGUMENT_USER_ID";
```

#### 2.2.15.1 Line-wrapping strategies

There isn't an exact formula that explains how to line-wrap and quite often different solutions are valid. However there are a few rules that can be applied to common cases.

__Break at operators__

The break comes __before__ the operator.

```java
int longName = anotherVeryLongVariable + anEvenLongerOne - thisRidiculousLongOne
        + theFinalOne;
```

__Assignment Operator Exception__

An exception to the `break at operators` rule is the assignment operator `=`, the line breaks __after__ the operator.

```java
int longName =
        anotherVeryLongVariable + anEvenLongerOne - thisRidiculousLongOne + theFinalOne;
```

__Method chain case__

When multiple methods are chained in the same line, every call to a method(except first) should go in its own line.

```java
Picasso.with(context)
        .load("http://ribot.co.uk/images/sexyjoe.jpg")
        .into(imageView);
```

__Long parameters case__

When a method has many parameters or its parameters are very long, we should break the line after every comma `,`

```java
loadPicture(context,
        "http://ribot.co.uk/images/sexyjoe.jpg",
        mImageViewProfilePicture,
        clickListener,
        "Title of the picture");
```

### 2.2.16 RxJava chains styling

Rx chains of operators require line-wrapping. Every operator must go in a new line and the line should be broken before the `.`

```java
public Observable<Location> syncLocations() {
    return databaseHelper.getAllLocations()
            .concatMap(new Func1<Location, Observable<? extends Location>>() {
                @Override
                 public Observable<? extends Location> call(Location location) {
                     return retrofitService.getLocation(location.getId());
                 }
            })
            .retry(new Func2<Integer, Throwable, Boolean>() {
                 @Override
                 public Boolean call(Integer numRetries, Throwable throwable) {
                     return throwable instanceof RetrofitError;
                 }
            });
}
```

## 2.3 XML style rules

### 2.3.2 Resources naming

#### 2.3.2.1 ID naming

| Element              | Prefix              |
| -------------------  | ------------------- |
| `TextView`           | `tv_`             |
| `ImageView`          | `iv_`            |
| `Button`             | `btn_`           |
| `Menu`               | `menu_`             |

#### 2.3.2.2 Strings

String names start with a prefix that identifies the section they belong to. For example `registration_email_hint` or `edit_profile_title`. If a string __doesn't belong__ to any section, then you may follow this rules:


| Prefix             | Description                           |
| -----------------  | --------------------------------------|
| `error_`           | An error message                      |
| `msg_`             | A regular information message         |
| `title_`           | A title, i.e. a dialog title          |
| `hint_`            | EditText hint		             |

<!---
## 2.4 Tests style rules

### 2.4.1 Unit tests
// todo
Test classes should match the name of the class the tests are targeting, followed by `Test`. For example, if we create a test class that contains tests for the `DatabaseHelper`, we should name it `DatabaseHelperTest`.

Test methods are annotated with `@Test` and should generally start with the name of the method that is being tested, followed by a precondition and/or expected behaviour.

* Template: `@Test void methodNamePreconditionExpectedBehaviour()`
* Example: `@Test void signInWithEmptyEmailFails()`

Precondition and/or expected behaviour may not always be required if the test is clear enough without them.

Sometimes a class may contain a large amount of methods, that at the same time require several tests for each method. In this case, it's recommendable to split up the test class into multiple ones. For example, if the `DataManager` contains a lot of methods we may want to divide it into `DataManagerSignInTest`, `DataManagerLoadUsersTest`, etc. Generally you will be able to see what tests belong together because they have common [test fixtures](https://en.wikipedia.org/wiki/Test_fixture).

-->

