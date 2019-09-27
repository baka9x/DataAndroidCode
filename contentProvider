package com.danghai.ps10201lab03;

import androidx.annotation.RequiresApi;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;

import android.Manifest;
import android.content.Intent;
import android.content.pm.PackageManager;
import android.database.Cursor;
import android.os.Build;
import android.os.Bundle;
import android.provider.Browser;
import android.provider.CallLog;
import android.provider.ContactsContract;
import android.provider.MediaStore;
import android.view.View;
import android.widget.Button;
import android.widget.ListView;
import android.widget.Toast;

import java.util.ArrayList;
import java.util.List;

public class MainActivity extends AppCompatActivity {

    private List contracts, callogs, media, bookmasks;

    private final int MY_PERMISSIONS_REQUEST_READ_CONTACTS = 990;
    private final int MY_PERMISSIONS_REQUEST_READ_CALLLOG = 991;
    private final int MY_PERMISSIONS_REQUEST_READ_MEDIA = 992;
    private final int MY_PERMISSIONS_REQUEST_READ_PHONE_STATE = 993;

    Button btnContact, btnCallog, btnMedia;

    @RequiresApi(api = Build.VERSION_CODES.M)
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        requestPermissionContacts();
        requestPermissionCalllog();
        requestPermissionMedia();

        btnContact = findViewById(R.id.btn_contact);
        btnCallog = findViewById(R.id.btn_call);
        btnMedia = findViewById(R.id.btn_media);
        btnContact.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                readAllContacts();
            }
        });
        btnCallog.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                readAllCallogs();
            }
        });
        btnMedia.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                readAllMedia();
            }
        });




    }

    //retrieve all contracts
    private void readAllContacts() {
        Cursor cursor = getContentResolver()
                .query(ContactsContract.Contacts.CONTENT_URI,
                        null, null, null, null);
        contracts = new ArrayList();
        int nameIndex = cursor.getColumnIndex(ContactsContract.Contacts.DISPLAY_NAME);
        while (cursor.moveToNext()) {
            contracts.add(cursor.getString(nameIndex));

        }
        Toast.makeText(this, "Size: " + contracts.size(), Toast.LENGTH_SHORT).show();
    }

    //retrieve all Call logs
    @RequiresApi(api = Build.VERSION_CODES.M)
    private void readAllCallogs() {
        if (checkSelfPermission(Manifest.permission.READ_CALL_LOG) != PackageManager.PERMISSION_GRANTED) {
            return;
        }
        Cursor cursor = getContentResolver()
                .query(CallLog.Calls.CONTENT_URI,
                        null, null, null, null);
        callogs = new ArrayList();
        int nameIndex = cursor.getColumnIndex(CallLog.Calls.NUMBER);
        while (cursor.moveToNext()){
            callogs.add(cursor.getString(nameIndex));

        }
        Toast.makeText(this, "Size: " + callogs.size(), Toast.LENGTH_SHORT).show();
    }
    //retrieve all Media
    private void readAllMedia() {
        Cursor cursor = getContentResolver()
                .query(MediaStore.Images.Media.EXTERNAL_CONTENT_URI,
                        null, null, null, null);
        media = new ArrayList();
        int nameIndex = cursor.getColumnIndex(MediaStore.Images.Media.DISPLAY_NAME);
        while (cursor.moveToNext()){
            media.add(cursor.getString(nameIndex));

        }
        Toast.makeText(this, "Size: " + media.size(), Toast.LENGTH_SHORT).show();
    }
    //retrieve all Media
    /*private void readAllBookmark() {
        Cursor cursor = getContentResolver()
                .query(Browser.,
                        null, null, null, null);
        media = new ArrayList();
        int nameIndex = cursor.getColumnIndex(MediaStore.Images.Media.DISPLAY_NAME);
        while (cursor.moveToNext()){
            media.add(cursor.getString(nameIndex));

        }
        Toast.makeText(this, "Size: " + media.size(), Toast.LENGTH_SHORT).show();
    }*/
    private void requestPermissionContacts(){
        // Here, thisActivity is the current activity
        if (ContextCompat.checkSelfPermission(this,
                Manifest.permission.READ_CONTACTS )
                != PackageManager.PERMISSION_GRANTED) {

            // Permission is not granted
            // Should we show an explanation?
            if (ActivityCompat.shouldShowRequestPermissionRationale(this,
                    Manifest.permission.READ_CONTACTS)) {
                // Show an explanation to the user *asynchronously* -- don't block
                // this thread waiting for the user's response! After the user
                // sees the explanation, try again to request the permission.
            } else {
                // No explanation needed; request the permission
                ActivityCompat.requestPermissions(this,
                        new String[]{Manifest.permission.READ_CONTACTS},
                        MY_PERMISSIONS_REQUEST_READ_CONTACTS);

                // MY_PERMISSIONS_REQUEST_READ_CONTACTS is an
                // app-defined int constant. The callback method gets the
                // result of the request.
            }
        } else {
            // Permission has already been granted
        }
    }
    private void requestPermissionCalllog(){
        if (ContextCompat.checkSelfPermission(this,
                Manifest.permission.READ_CALL_LOG )
                != PackageManager.PERMISSION_GRANTED) {
            if (ActivityCompat.shouldShowRequestPermissionRationale(this,
                    Manifest.permission.READ_CALL_LOG)) {
            } else {
                // No explanation needed; request the permission
                ActivityCompat.requestPermissions(this,
                        new String[]{Manifest.permission.READ_CALL_LOG},
                        MY_PERMISSIONS_REQUEST_READ_CALLLOG);
            }
        } else {
        }
    }
    private void requestPermissionMedia(){
        if (ContextCompat.checkSelfPermission(this,
                Manifest.permission.READ_EXTERNAL_STORAGE )
                != PackageManager.PERMISSION_GRANTED) {
            if (ActivityCompat.shouldShowRequestPermissionRationale(this,
                    Manifest.permission.READ_EXTERNAL_STORAGE)) {
            } else {
                ActivityCompat.requestPermissions(this,
                        new String[]{Manifest.permission.READ_EXTERNAL_STORAGE},
                        MY_PERMISSIONS_REQUEST_READ_MEDIA);
            }
        } else {
        }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode,
                                           String[] permissions, int[] grantResults) {
        switch (requestCode) {
            case MY_PERMISSIONS_REQUEST_READ_CONTACTS:
            case MY_PERMISSIONS_REQUEST_READ_CALLLOG:
            case MY_PERMISSIONS_REQUEST_READ_MEDIA: {
                // If request is cancelled, the result arrays are empty.
                if (grantResults.length > 0
                        && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                    // permission was granted, yay! Do the
                    // contacts-related task you need to do.
                } else {
                    // permission denied, boo! Disable the
                    // functionality that depends on this permission.
                }
                return;
            }

            // other 'case' lines to check for other
            // permissions this app might request.
        }
    }






}
