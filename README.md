# android-phone-number-input

android-phone-number-input is A small UI library that allows you to create phone fields with corresponding country flags, and validate the phone number using libphonenumber from google. This project aar file was published using Jitpack.


<img src="https://raw.githubusercontent.com/dylansalim3/android-phone-number-input/master/raw/phone-field.gif" alt="alt text" title="Sample App" style="max-width:100%;">

# The library has two different fields:

# 1.PhoneEditText : 
includes EditText alongside the flags spinner

# 2.PhoneInputLayout : 
includes a TextInputLayout from the design support library alongside the flags spinner

# Features

Displays the correct country flag if the user enters a valid international phone number
Allows the user to choose the country manually and only enter a national phone number
Allows you to choose a default country, which the field will change to automatically if the user chose a different country then cleared the field.

## Validates the phone number
Returns the valid phone number including the country code

# Dependencies
- com.google.android.material:material:1.2.1
- com.googlecode.libphonenumber:libphonenumber:8.12.14


# Usage

# 1. Import the project in Android Studio.
- Add the following to the root build.gradle
```
  allprojects {
    repositories {
        ...
        maven { url 'https://jitpack.io' }
    }
}

```
- Add the dependency at the app level build.gradle

```
dependencies {
	        implementation 'com.github.dylansalim3:android-phone-number-input:1.0.3'
	}
```


# 2.In your layout you can use the PhoneInputLayout

```
<com.dylan.phoneNumberInput.PhoneInputLayout
     android:id="@+id/phone_input_layout"
     android:layout_width="match_parent"
     android:layout_height="wrap_content"/>
  ```
   
   
//or the PhoneEditText
```

 <com.dylan.phoneNumberInput.PhoneEditText
     android:id="@+id/edit_text"
     android:layout_width="match_parent"
     android:layout_height="wrap_content"/>
     
```

     
# 3.Then in your Activity/Fragment

```

     
final PhoneInputLayout phoneInputLayout = (PhoneInputLayout) findViewById(R.id.phone_input_layout);
final PhoneEditText phoneEditText = (PhoneEditText) findViewById(R.id.edit_text);
final Button button = (Button) findViewById(R.id.submit_button);
```

// you can set the hint as follows
```

phoneInputLayout.setHint(R.string.phone_hint);
phoneEditText.setHint(R.string.phone_hint);
```

// you can set the default country as follows
```

phoneInputLayout.setDefaultCountry("DE");
phoneEditText.setDefaultCountry("FR");
button.setOnClickListener(new View.OnClickListener() {
  @Override
  public void onClick(View v) {
    boolean valid = true;
    
    // checks if the field is valid 
    if (phoneInputLayout.isValid()) {
      phoneInputLayout.setError(null);
    } else {
      // set error message
      phoneInputLayout.setError(getString(R.string.invalid_phone_number));
      valid = false;
    }

    if (phoneEditText.isValid()) {
      phoneEditText.setError(null);
    } else {
      phoneEditText.setError(getString(R.string.invalid_phone_number));
      valid = false;
    }

    if (valid) {
      Toast.makeText(MainActivity.this, R.string.valid_phone_number, Toast.LENGTH_LONG).show();
    } else {
      Toast.makeText(MainActivity.this, R.string.invalid_phone_number, Toast.LENGTH_LONG).show();
    }
    
    // Return the phone number as follows
    String phoneNumber = phoneInputLayout.getPhoneNumber();
  }
  
});

```

 
# Customization

In case the default style doesn't match your app styles, you can extend the PhoneInputLayout, or PhoneEditText and provide your own xml, but keep in mind that you have to provide a valid xml file with at least an EditText (tag = phonefield_edittext) and Spinner (tag = phonefield_flag_spinner), otherwise the library will throw an IllegalStateException.

You can also create your own custom view by extending the PhoneField directly.

# Note:
If you find newly issued mobile numbers not validated as mobile number for any country you can add supporting them by using latest dependancy of 

<code> compile 'com.googlecode.libphonenumber:libphonenumber:X.X.X'  </code>

in your android-phonefield-Input gradle.
So that this library will support latest issued numbers.

# Example senario:

For library whis is using com.googlecode.libphonenumber:libphonenumber:7.X.X  versions ,
JIO numbers starting with 89XXX XXXXX was not a mobile number in India.
but when i migrated to com.googlecode.libphonenumber:libphonenumber:8.X.X  support was there.

You can check latest <a href="https://github.com/googlei18n/libphonenumber">Here</a>


