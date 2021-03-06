# Pool Products


### Installing Sceneform

* **Step1** 

First you need to install Sceneform plugin.
Go to android Studio: 
go to File -> Settings ->  Plugins -> Search for sceneform -> Install it

* **Step2**

Copy the sampledata  directory in the app folder and place it in your project
Go in the models folder and delete all the sfa files

* **Step3**

Right click on the .obj files 
click on Import Sceneform assest
And then click Ok in the dialog box to import it

* **Step4**

Add these lines in manifest.xml file
meta-data tag will go inside application tag

```xml

<uses-feature
        android:name="android.hardware.camera.ar"
        android:required="true" />

<meta-data
            android:name="com.google.ar.core"
            android:value="required" />
```

* **Step5**

This is the image view in the ObjectActivity on clicking which you will be sent to ARActivity
```java
ImageView bed=(ImageView) findViewById(R.id.bed);
        bed.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Toast.makeText(v.getContext(),"bed Clicked",Toast.LENGTH_SHORT).show();
                Intent intent=new Intent(ObjectActivity.this, ARActivity.class);
                intent.putExtra("object","bed");
                startActivity(intent);

            }
        });
```
In this case The imageview id is Bed. We set a Listener on it. The moment it is clicked we define the variable intent. But there is an extra also put in this intent.
While going to the ARActivity you see the line 
```java
Intent intent=new Intent(ObjectActivity.this, ARActivity.class);
                
```
This line will tell the ARActivity that the **Object** to be deployed is a __Bed__
```java 
intent.putExtra("object","bed");
```


then we start the intent
```java
startActivity(intent);
```


* **Step6**

How to receive the Object at the ARActivity

These three lines will give the variable **object** the value of the _item to be deployed_
In this particular case the variable **object** has the value _"bed"_
```java
Intent i = getIntent();
Bundle b = i.getExtras();
String object = (String) b.get("object");
```



After this using the value of the **object** value we decide the name of the model to be launched
The following code goes in ARActivity
```java
if (object.equals("bed")) {
            fragment.setOnTapArPlaneListener(new BaseArFragment.OnTapArPlaneListener() {
                @Override
                public void onTapPlane(HitResult hitResult, Plane plane, MotionEvent motionEvent) {
                    addObject(Uri.parse("Bed_01.sfb"));
                }
            });

        }
```

this line
Fires up a series of functions which uses the model **"Bed_01.sfb"** to deploy it on the screen
```java
addObject(Uri.parse("Bed_01.sfb"));
```
