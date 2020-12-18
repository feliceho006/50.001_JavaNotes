# Week 11 Lesson

#### Intent - `startActivityForResult()`

- **Explicit intents** bring you from one activity to another, data can be passed.
- **Implicit intent** bring you from one activity to another component in your app. You specify what component you want.

In both cases, you launch `startActivity(intent);`

> Explicit Intent - startActivityForResult()
1. Declare request code
2. Declare explicit intent
3. In destination, user interact with it
4. User action bring user back to original activity
5. In original activity, override callback `onActivityResult()`

```java=
final int REQUEST_CODE_IMAGE = 1000;

Intent intent = new Intent(MainActivity.this, DataEntry.class);
startActivityForResult(intent, REQUEST_CODE_IMAGE);



@Override
protected void onActivityResult(int request code, inte resultCode, Intent data){
    if (requestCode ==Acitivity.CODE_IMG){
        if (resultCode ==Acitivity.RESULT ){
            double value = data.getDoubleExtra(DataEntry, KEY)
        }
        
    Toast.makeText(this, "message", Toast.LENGTH).show;
    
    if (resultCode == Activity.RESULT_CANCELED){
    }
    }
    
}
```

```java=
Intent returnIntent = new Intent();
returnIntent.putExtra(KEY, value);
setResult(Acitivity.RESULT_OK, returnintent); //Acitivity.RESULT_CANCELLED, user backed out
finish();
```

#### Strategy Design Pattern
```java=
public abstract class Duck{
    private Fly fly;

    private Quack quack;

    String name;

    public Duck(){
    }

    public Duck(String name){
        this.name = name;
    }

    public void setFly(Fly fly){
        this.fly = fly;
    }

    public void setQuack(Quack quack){
        this.quack = quack
    }

    public void performFly(){
        fly.fly();
    }
    
    public abstract void display;
}
```

- Flying is delegated to a Fly object
- Quacking is delegated to a Quack object

for Fly
```java=
interface Fly{
    void fly();
}

class Flapwings implements Fly{
    @Override
    public void fly(){
        Systerm.out.println("Flappinh my wings");
    }
}    
    
    public interface Quack{
        void quack();
    }
public class Logbook implements Quack{
    @Overrude
    public void quack(){
        System.out.println("Quack");
    }
} 
}
```
subclass duck with own object

```java=
public class MallardDuck extends Duck {
    MallardDuck(String name){
        super(name);
    }
    
    @Override
    public void display(){
        System.out.println("I am" + name + ", the         Matters")
    }
}
```
```java=
public class TestDuck{
    public static void main(String[] args){
        Duck duck new MallardDuck("Donals")
        duck.setFlyBehaviour(new LoudQuack());
        duck.setQuackBehaviour(new LoudQuack());
        duck.display();
        duck.performFly()
        duck.performQuack()
    }
}
```

We see here the flexibility of composition over inheritance. We develop our duck behaviours independent of the type of duck. The behaviour of the duck is delegated to separate objects.

#### Adapter Design Pattern

The word `interface` is an overloaded word 
- in Java terminology it would mean a type of class with method signatures only 
- it could also mean the set of methods that a class allows you to access (think of ‘user interface’)

An adapter design pattern converts the interface of one class into another that a client class expects.

```java=
public interface Duck { 
 void quack (); 
 void fly (); 
}
```
```java=
public class MallardDuck implements Duck { 
 @Override 
 public void quack() { 
     System.out.println( "Mallard Duck says Quack" ); 
 } 
 @Override 
 public void fly() {
     System.out.println( "Mallard Duck is flying" ); 
 } 
}
```
Then you have a client that loops through all ducks and makes them fly and quack.
```java=
import java.util.ArrayList; 
public class DuckClient { 
 static ArrayList<Duck> myDucks; 
 
 public static void main (String[] args){ 
     myDucks = new ArrayList<>(); 
     myDucks.add( new MallardDuck()); 
     makeDucksFlyQuack(); 
 } 
 static void makeDucksFlyQuack(){ 
     for (Duck duck: myDucks){ 
         duck.fly(); 
         duck.quack(); 
     } 
 } 
}
```
```java=
public interface Turkey { 
     public void gobble (); 
     public void fly (); 
}
```
```java=
public class TurkeyAdapter implements Duck { 
     Turkey turkey; 
     TurkeyAdapter(Turkey turkey){ 
         this.turkey = turkey; 
     } 
     
 @Override 
 public void quack () { 
 //implement this 
 } 
 @Override 
 public void fly () { 
 //implement this 
 } 
}
```
![](https://i.imgur.com/EDVm7Up.png)

#### RecyclerView
Allows the user to scroll through the data.
```java=
ArrayList<Integer> drawableId = new ArrayList<>();
dataSource = Utils.firstLoadImages(this, drawableId);

charaAdapter = new CharaAdapter( this, dataSource);
recyclerView.setAdapter( charaAdapter);
/** Explore using new GridLayoutManager */
recyclerView.setLayoutManager(new LinearLayoutManager(this));
```

Writing an adapter
```java=
public class CharaAdapter extends RecyclerView.Adapter<CharaAdapter.CharaViewHolder>{

    Context context;
    LayoutInflater mInflater;
    DataSource dataSource;

    CharaAdapter(Context context, DataSource dataSource){
        mInflater = LayoutInflater.from(context);
        this.context = context;
        this.dataSource = dataSource;
    }

    @NonNull
    @Override
    public CharaViewHolder onCreateViewHolder(@NonNull ViewGroup viewGroup, int i) {
        View itemView = mInflater.inflate(R.layout.pokemon, viewGroup,
                false);
        return new CharaViewHolder(itemView);
    }

    @Override
    public void onBindViewHolder(@NonNull CharaViewHolder charaViewHolder, int i) {
        charaViewHolder.textViewName.setText(  dataSource.getName(i));
        charaViewHolder.imageViewChara.setImageBitmap(
                dataSource.getImage(i));
    }

    @Override
    public int getItemCount() {
        return dataSource.getSize();
    }

    static class CharaViewHolder extends RecyclerView.ViewHolder{

        ImageView imageViewChara;
        TextView textViewName;

        CharaViewHolder(View view){
            super(view);
            imageViewChara = view.findViewById(R.id.cardViewImage);
            textViewName = view.findViewById(R.id.cardViewTextName);
        }
    }
}
```
Swiping to delete
```java=
void removeData(int i){
    dataArrayList.remove(i);
}

ItemTouchHelper itemTouchHelper = new ItemTouchHelper(simpleCallback);
itemTouchHelper.attachToRecyclerView(recyclerView);

ItemTouchHelper.SimpleCallback simpleCallback = new 
ItemTouchHelper.SimpleCallback( 0 , ItemTouchHelper.LEFT | 

ItemTouchHelper.RIGHT ) { 
     @Override 
     public boolean onMove (@NonNull RecyclerView recyclerView, 
    @NonNull RecyclerView.ViewHolder viewHolder, @NonNull 
    RecyclerView.ViewHolder viewHolder1) { 
     return false ; 
     }
     
     @Override 
     public void onSwiped (@NonNull RecyclerView.ViewHolder viewHolder, int i) { 
     //code to delete the view goes here 
     CharaAdapter.CharaViewHolder charaViewHolder = (CharaAdapter.CharaViewHolder) viewHolder;
     int position = charaViewHolder.getAdapterPosition();
     dataSource.removeData(position);
     
     charaAdapter.notifyDataSetChanged();
     
     } 
}
```

### Static Class
```java
public class MyClass {

	// get this by using MyClass.counter()
	// can have static in outer class but not in inner class thats not static
	// can have static var in outer class but not in inner

	static boolean counter(){
		return true;
	}

    public static void main(String[] args) {
	
	//	you only call a non static method from a static context, in a nested
	//  static class

	//  high high2 = new high();
	//   when it is static, you dont need a new obj to call the mtd
        boolean hi = high.isHigh(new Felia(3));
        System.out.println(hi);
		
		high high2 = new high();
		boolean ok = high2.isOk(new Felia(8));
    }

    static class high{
		double y; // can have non static inside
        static int i; // can also have static

        static boolean isHigh(Felia felia){
            if (felia.getTime() < 8){
                return true;
            } else{
                return false;
            }
        }
		
		boolean isOk(Felia felia){
            if (felia.getTime() < 8){
                return false;
            } else{
                return true;
            }
        }

    }

    static class Felia {
//        private int time;
        static int time;

        Felia(int time){
            this.time = time;
		}
}
}
        
```