# Pool Products

### Objective

Pool Product is a app which deploys 3D objects in real World depending on the Object Image You clicked.

### Activities

Poop product consist of two activities

* ObjectActivity _(Temporary activity)_
The activity in which images are displayed. These images when clicked sends you to the MainActivity

* MainActivity
The main camera activity in which the object will be deployed in real world after tapping the screen

### How to integrate 

Assuming you have an Image in any activity. So the process of Clicking that image and deploying that object on your screen happens in this way

* **Step1**

This is the image view in the ObjectActivity on clicking which you will be sent to MainActivity
```java
ImageView bed=(ImageView) findViewById(R.id.bed);
        bed.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Toast.makeText(v.getContext(),"bed Clicked",Toast.LENGTH_SHORT).show();
                Intent intent=new Intent(ObjectActivity.this, MainActivity.class);
                intent.putExtra("object","bed");
                startActivity(intent);

            }
        });
```
In this case The imageview id is Bed. We set a Listener on it. The moment it is clicked we define the variable intent. But there is an extra also put in this intent.
While going to the MainActivity you see the line 
```java
Intent intent=new Intent(ObjectActivity.this, MainActivity.class);
                
```
This line will tell the MainActivity that the **Object** to be deployed is a __Bed__
```java 
intent.putExtra("object","bed");
```


then we start the intent
```java
startActivity(intent);
```


* **Step2**

How to receive the Object at the MainActivity

These three lines will give the variable **object** the value of the _item to be deployed_
In this particular case the variable **object** has the value _"bed"_
```java
Intent i = getIntent();
Bundle b = i.getExtras();
String object = (String) b.get("object");
```



After this using the value of the **object** value we decide the name of the model to be launched
The following code goes in MainActivity
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
