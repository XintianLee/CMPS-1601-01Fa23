## Q1
```java
class Workshop {  
    public static void main(String[] args) {  
        var hammer = new Tool();  
        var carpenter = new Carpenter("Mark", hammer);  
    }  
}

class Carpenter {  
    String name;  
    Tool favoriteTool;
    _________________________ {  
        this.name = name;  
        this.favoriteTool = favoriteTool;  
    }  
}  
class Tool{}
```
> [!info]
> See [[Lab 01 - Objects & Classes#Special member methods|Constructor]].
- The constructor is usually `public` if the class is allowed to be instantiate.
- Referring to Line 4, where a `Carpenter` object is initialized, and the body of the constructor, the answer should be `public Carpenter(String name, Tool favoriteTool)`.

## Q2
```java
class MessagingApp {  
    public static void main(String[] args) {  
       var user1 = new User();  // (1)
       user1.sendMessage();  // (4)
    }  
}

abstract class AppUser{  
    int messagesSent;  
    public AppUser(int messagesSent){  
        this.messagesSent = messagesSent;  // (3)
    }  
    public void sendMessage(){  
        System.out.println("Sending "+countMessages(5)+" messages");  // (5)
    }  
    public abstract int countMessages(int additionalMessages);  
}  
class User extends AppUser{  
    public User(){  
        super(10);  // (2) calling base class constructor
    }  
      
    public int countMessages(int additionalMessages){  // @Override
        return messagesSent + additionalMessages;  // (6)
    }  
}
```
> [!info]
> See [[Lab 04 - Abstract Classes & Interfaces#Abstract Class|Abstract Class]].
- `(1)(2)(3)`: `user1.messagesSent` is set to $10$
- `(4)(5)(6)`: `countMessages(5)` returns $10 + 5 = 15$

## Q3
```java
class Machines {  
    public static void main(String[] args) {  
       _________________________;  
       for(var device: devices){  
           device.print();  
       }  
    }  
}

interface Device{  
    public void operate();  
}  
class Scanner implements Device{  
    public void operate(){  
        System.out.println("Scanner is scanning");  
    }  
    public void scan(){  
        System.out.println("Scanner is performing a scan");  
    }  
}  
class Printer implements Device{  
    public void operate(){  
        System.out.println("Printer is printing");  
    }  
    public void print(){  
        System.out.println("Printer is printing a document");  
    }  
}
```
> [!info]
> See [[Lab 03 - Generics#ArrayList|ArrayList]].
- In the *for*-loop, method `print` is called, which means the device should be a `Printer`.
- Some valid definitions:
  - `var devices = new ArrayList<Printer>()`
  - `ArrayList<Printer> devices = new ArrayList<>()`

## Q4
```java
class Carpenter {
    private Service service;
    public Service getService() {
        return service;
    }
    public void Provide(Service service) {
        Build(service);
    }
    public void Build(Service service) {
        this.service = service;
    }
}

class Plumber {
    private Service service;
    public Service getService() {
        return service;
    }
    public void Provide(Service service) {
        Replace(service);
	}
    public void Replace(Service service) {
        this.service = service;
	}
}
```
- `Carpenter` and `Plumber` both have a method `void Provide(Service)`
  ```java
  interface Provider {
      public void Provide(Service service);
  }
  ```

## Q5
```java
class Mixer <T1, T2> {
    private T1 a;
    public T1 getA() {
        return a;
    }
    private T2 b;
    public T2 getB() {
        return b;
    }
    public Mixer(T1 a, T2 b) {
        this.a = a;
        this.b = b;
    }
    public String combine() {
        return String.valueOf(a) + String.valueOf(b);
    }
}
```
> [!info]
> See [[Lab 03 - Generics#Generic class example|Generic class]].

## Q6
```java
class Main {
    public static void main(String[] args) {
       IGame game1 = new Game();
       Player player1 = new Player("Alex");
       Player player2 = new Player("Anna");
       player1.play(game1, player2); // (1)
       System.out.println("Playing against: "+ ((Game)game1).getOpponent());
    }
}

class Player{
    String name;
    public Player(String name){
        this.name = name;
    }
    public void play(IGame game, Player other){
        game.play(this, other); // (2) Polymorphism
    }
    public String toString(){
        return name;
    }
}

interface IGame{
    public void play(Player p1, Player p2);
}

class Game implements IGame{
    Player p1, p2;
    public void play(Player p1, Player p2){ // (3)
        this.p1=p1;
        this.p2=p2;
    }
    public Player getPlayer(){return p1;}
    public Player getOpponent(){ return p2; }
}
```