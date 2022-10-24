# FILE APPLICATION , CREATE AND SAVE TEXT FILE USING ANDROID STUDIO

#~   activity_main_xml ~ code

<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#E8F5E9"

    tools:context=".MainActivity"
    tools:ignore="ExtraText">

    <Button
        android:id="@+id/buttonsave"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:background="#FFCDD2"
        android:backgroundTint="#FFF9C4"
        android:text="SAVE"
        android:textAppearance="@style/TextAppearance.AppCompat.Medium"
        android:textColor="#795548"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.461"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.976"
        app:strokeColor="#F8BBD0" />

    <Button
        android:id="@+id/buttonopen"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:background="#FFCDD2"
        android:backgroundTint="#FFF9C4"
        android:text="OPEN"
        android:textAppearance="@style/TextAppearance.AppCompat.Medium"
        android:textColor="#795548"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.869"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.25"
        app:strokeColor="#F8BBD0" />

    <Button
        android:id="@+id/buttoncreate"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:background="#FFCDD2"
        android:backgroundTint="#FFF9C4"
        android:text="CREATE"
        android:textAppearance="@style/TextAppearance.AppCompat.Medium"
        android:textColor="#795548"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.111"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.251"
        app:rippleColor="@color/cardview_dark_background"
        app:strokeColor="#FFCDD2" />

    <EditText
        android:id="@+id/editText"
        android:layout_width="249dp"
        android:layout_height="66dp"
        android:ems="10"
        android:gravity="start|top"
        android:hint="@string/app_name"
        android:inputType="textMultiLine"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.497"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.863" />

    <TextView
        android:id="@+id/textView2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:fontFamily="sans-serif-condensed-medium"
        android:text="~ FILE APPLICATION ~"
        android:textColor="#BF6DCD"
        android:textSize="15pt"
        android:textStyle="italic"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.095" />

    <ImageView
        android:id="@+id/imageView4"
        android:layout_width="379dp"
        android:layout_height="251dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.577"
        app:srcCompat="@drawable/pandasecurity_android_messages" />

</androidx.constraintlayout.widget.ConstraintLayout>



#~ MAINACTIVITY.java code ~





package com.example.myapplication;
import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;
import java.io.BufferedReader;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStreamReader;
import java.nio.charset.StandardCharsets;

public class MainActivity extends AppCompatActivity {
    Button btncreate,btnopen,btnsave;
    EditText txtinput;
    private static final String FILE_NAME="example.txt";
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        txtinput=findViewById(R.id.editText);
        btncreate=findViewById(R.id.buttoncreate);
        btnopen=findViewById(R.id.buttonopen);
        btnsave=findViewById(R.id.buttonsave);
        btncreate.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View V) {
                String text=txtinput.getText().toString();
                FileOutputStream fos=null;
                try{
                    fos=openFileOutput(FILE_NAME,MODE_PRIVATE);
                    fos.write(text.getBytes());
                    txtinput.getText().clear();
                    Toast.makeText(MainActivity.this,"Saved to"+getFilesDir()+"/"+FILE_NAME,Toast.LENGTH_LONG).show();
                } catch (FileNotFoundException e) {
                    e.printStackTrace();
                }
                catch (IOException e)
                {
                    e.printStackTrace();
                }
                finally {
                    if(fos != null)
                    {
                        try{
                            fos.close();
                        }
                        catch (IOException e)
                        {
                            e.printStackTrace();
                        }
                    }
                }


            }


        });
        btnopen.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View V) {
                FileInputStream fis=null;
                try {
                    fis = openFileInput(FILE_NAME);
                    InputStreamReader isr = new InputStreamReader(fis);
                    BufferedReader br = new BufferedReader(isr);
                    StringBuilder sb = new StringBuilder();
                    String text;
                    while ((text=br.readLine()) != null)
                    {
                        sb.append(text).append("\n");

                    }
                    txtinput.setText(sb.toString());
                }
                catch (FileNotFoundException e)
                {
                    e.printStackTrace();
                }
                catch (IOException e)
                {
                    e.printStackTrace();
                }
                finally {
                    if (fis != null)
                    {

                            try {
                                fis.close();
                            } catch (IOException e) {
                                e.printStackTrace();
                            }

                    }
                }
            }
        });
        btnsave.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View V) {
                String text = txtinput.getText().toString();
                if (text.isEmpty()) {
                    Toast.makeText(MainActivity.this,"First Create the File", Toast.LENGTH_LONG).show();
                }
                else {
                    FileOutputStream fss = null;
                    try {
                        fss = openFileOutput(FILE_NAME,MODE_PRIVATE);
                        fss.write(text.getBytes());
                        txtinput.getText().clear();
                        Toast.makeText(MainActivity.this,"Saved to"+getFilesDir()+"/"+FILE_NAME,Toast.LENGTH_LONG).show();
                    }
                    catch (FileNotFoundException e)
                    {
                        e.printStackTrace();
                    }
                    catch (IOException e) {
                        e.printStackTrace();
                    }
                    finally {
                        if (fss != null) {
                            try {
                                fss.close();
                            } catch (IOException e) {
                                e.printStackTrace();
                            }
                        }
                    }
                }
            }
        });

    }
}
