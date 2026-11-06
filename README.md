# Ex.No:2(b) To create a two screens , first screen will take one number input from user. After click on Factorial button, second screen will open and it should display factorial of the same number using Explicit Intents.


## AIM:

To create a two screens , first screen will take one number input from user. After click on Factorial button, second screen will open and it should display factorial of the same number using Explicit Intents.


## EQUIPMENTS REQUIRED:

Latest Version Android Studio

## ALGORITHM:



## PROGRAM:
```
/*
Program to print the text “ExplicitIntent”.
Developed by: Kishore R
Registeration Number : 212225040192
*/
```
## MainActivity.java
```
package com.example.explicit;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.os.Bundle;
import android.widget.Button;
import android.widget.EditText;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        EditText editText = findViewById(R.id.editTextText);
        Button button = findViewById(R.id.button);

        button.setOnClickListener(v -> {
            String num = editText.getText().toString().trim();
            if (num.isEmpty()) {
                editText.setError(getString(R.string.invalid_input));
                return;
            }
            Intent intent = new Intent(MainActivity.this, MainActivity2.class);
            intent.putExtra("number", num);
            startActivity(intent);
        });
    }
}


```
## Activity_Main.xml
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:padding="24dp"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/tvTitle"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="32dp"
        android:text="@string/explicit_title"
        android:textColor="?attr/colorPrimary"
        android:textSize="28sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toTopOf="@+id/textView"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_chainStyle="packed" />

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="16dp"
        android:text="@string/enter_a_number"
        android:textColor="?attr/colorOnBackground"
        android:textSize="18sp"
        app:layout_constraintBottom_toTopOf="@+id/editTextText"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/tvTitle" />

    <EditText
        android:id="@+id/editTextText"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginStart="32dp"
        android:layout_marginEnd="32dp"
        android:layout_marginBottom="24dp"
        android:autofillHints=""
        android:ems="10"
        android:gravity="center"
        android:hint="@string/number_hint"
        android:inputType="number"
        android:textSize="18sp"
        app:layout_constraintBottom_toTopOf="@+id/button"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textView" />

    <com.google.android.material.button.MaterialButton
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:paddingHorizontal="24dp"
        android:paddingVertical="12dp"
        android:text="@string/find_factorial"
        android:textSize="16sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/editTextText" />

</androidx.constraintlayout.widget.ConstraintLayout>


```
## MainActivity2.java
```
package com.example.explicit;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.os.Bundle;
import android.widget.Button;
import android.widget.TextView;

import java.math.BigInteger;

public class MainActivity2 extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main2);

        TextView result = findViewById(R.id.result);
        Button btnHome = findViewById(R.id.btnHome);

        String number = getIntent().getStringExtra("number");
        if (number != null && !number.trim().isEmpty()) {
            try {
                int n = Integer.parseInt(number.trim());
                if (n < 0 || n > 1000) {
                    result.setText(R.string.invalid_input);
                } else {
                    BigInteger fact = BigInteger.ONE;
                    for (int i = 2; i <= n; i++) {
                        fact = fact.multiply(BigInteger.valueOf(i));
                    }
                    result.setText(getString(R.string.factorial_result, n, fact.toString()));
                }
            } catch (NumberFormatException e) {
                result.setText(R.string.invalid_input);
            }
        } else {
            result.setText(R.string.invalid_input);
        }

        btnHome.setOnClickListener(v -> {
            if (isTaskRoot()) {
                Intent intent = new Intent(MainActivity2.this, MainActivity.class);
                startActivity(intent);
            }
            finish();
        });
    }
}


```
## Activity_Main2.xml
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:padding="24dp"
    tools:context=".MainActivity2">

    <TextView
        android:id="@+id/result"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_marginBottom="32dp"
        android:gravity="center"
        android:text="@string/factorial"
        android:textColor="?attr/colorOnBackground"
        android:textSize="24sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toTopOf="@+id/btnHome"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_chainStyle="packed" />

    <com.google.android.material.button.MaterialButton
        android:id="@+id/btnHome"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:paddingHorizontal="24dp"
        android:paddingVertical="12dp"
        android:text="@string/go_to_home_screen"
        android:textSize="16sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/result" />

</androidx.constraintlayout.widget.ConstraintLayout>


```

## OUTPUT

<img width="1917" height="1078" alt="image" src="https://github.com/user-attachments/assets/7ac99f12-fb44-4c03-9e1c-e195e7a8da1f" />
<img width="1912" height="1078" alt="image" src="https://github.com/user-attachments/assets/7ac0a251-0564-4be9-be23-4df0575a260a" />
<img width="1917" height="1077" alt="image" src="https://github.com/user-attachments/assets/4365bc74-96b5-4b30-a3e3-9213f1e92845" />
<img width="1917" height="1078" alt="image" src="https://github.com/user-attachments/assets/672acf61-60d0-4cd9-b6a0-b13edead271a" />





## RESULT
Thus a Simple Android Application create a Explicit Intents using Android Studio is developed and executed successfully.


