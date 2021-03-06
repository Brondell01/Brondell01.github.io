## Welcome to Jeff's Portfolio

As you explore this ePortfolio please recognize that it has been designed with a purpose. The intent here is to provide a working example of my personal skill set combined with a professional level presentation. The following sections will first introduce you to who I am as a developer, and then move on into the skill-based portions of this portfolio.

For this portfolio and its different sections, I've focused on updating an existing data artifact I had developed for one of my higher level SNHU courses. Throughout this page you will different enhancements I've made to a simple Inventory Application, which has been designed for an android mobile device. These enhancements will showcase skills in the areas of Software Design and Engineering, Algorithms and Data Structures, and finally Databases. The end result will hopefully show you not only a proficiency within these targeted areas, but also a more robust and professional approach to developing skills necessary for any role within the industry. 

## Jeff as a Programmer
Throughout my time at SNHU I've had plenty of opportunities to produce code and develop applications. Each of my assignments was initially developed with a "pass this class" mentality. However, given more time, I've had a chance to reflect on my experience and hone in on who I am as a developer and how my skills fit within the program as it's been defined. This is where we discuss how I approach and solve problems, as well as apply focus on the more specific skill set, I bring to the role of software developer. 

As this ePortfolio will show, I have more than a competent level of skill when it comes to working with code and the different nuanced approaches that are required to get it to function.  First among all considerations is "does it work?", following this question any developer will understand and appreciate the numerous ways that any problem can be solved. As I've worked through SNHU and more specifically, through this course, I’ve come to recognize central tenants of my approach that aid in my success. 

I've learned that a formulaic approach helps to solve any problem, and that this view is essential to developing a working code base. At its core, developing code is essentially a codified response to a problem. We are trained and presented with tools, and are then asked to apply our knowledge and experience in a way that best solves a given requirement. My strength as a programmer comes from that process and the steps in which a problem is defined and broken down and then solved. 

you will see in the following sections that each "problem" has a different solution. The culmination of these solutions will represent a fully functional application. These solutions will clearly showcase a personal level of proficiency in utilizing both common and abstract standards and practices for developing code. More concrete illustrations will exist as you review this portfolio, but to provide an example we can focus on the change discussed in more detail with software Design and Engineering. A challenge presented itself in how I could display an expanding list of data to a user through the Android application UI. To solve this, I took advantage of my proficiency with different elements of software engineering and created an approach to displaying data in Java through the use of lists and iterations. As you view this portfolio please focus on these skill areas of focus, as these areas were intentionally over developed to highlight skills and solutions similar to the example provided above. 

#### Areas of Focus.
- [Software Design and Engineering](#software-design-and-engineering)
- [Data Structures and Algorithms](#data-structures-and-algorithms)
- [Databases](#database)

Beyond focusing on these specific areas, it is important for me to mention that there are other less obvious tools and skills at play here. A great deal of communication is required in any large project. It's difficult to showcase a "team" mentality on a personal project for school, but I would be a liar if I didn't include credit to the communication skills that made this possible. While maybe not traditional, using online resources that connect developers has proven to be a very important tool for me to build this application. Insights and direction have been gleaned through multiple interactions, and it is possible for others to comment on my work through the use of my Git profile for this project. A working example of this is the fact that my professor has had continual access to my gitHub profile. This allows others to review work and provide direction when necesary. These experiences closely align with those that a developer may encounter in a professional working environment.

These experiences have also exposed me to aspects of development that I initially found foreign, which includes secure coding. Fortunately, due to the strongly typed nature of Java as a development language we already have a greater level of control over aspects of our application, which extends certain protections to how our data is used. This protection is futher applied in how we interact with data in this application. As you'll see when we cover how the database is used, this application was designed to limit a user’s ability to "high-jack" our data. These two facts help illustrate how security is part of coding, and needs to be a more intential process as we design our programs.

## Code Review
For this artifact I've taken the time to run through a formal code review process of the Inventory Application. As stated, this application provides a great opportunity to showcase various skills. The code review here will set a functional baseline for the artifact as it stood prior to this course. It's important to remember that this artifact was created for a previous course and the planned enhancements I discuss in the review will not only improve the existing code base but expand its functionality to match the project requirements. 

As you will see in the following videos, a review of the code provides a great opportunity to identify potential improvements and gaps in logic, as well as refocusing attention on some of the smaller details associated with creating an application. As this Inventory Application currently stands, you will see a great deal of redundant code and a general lack of clarity in design. The code review video will walk you through my thought process as I identify needed improvements and plan my next steps. 

For viewing the Code Review see [Selected Artifact initial code review](https://snhu-my.sharepoint.com/personal/jeff_brondell_snhu_edu/_layouts/15/onedrive.aspx?id=%2Fpersonal%2Fjeff%5Fbrondell%5Fsnhu%5Fedu%2FDocuments%2FCode%20Review), or start by viewing the following video. 

[![This is an image](https://user-images.githubusercontent.com/61640483/144322045-40b010b1-8696-4cdf-b4db-8f92b1c2648d.png)](https://snhu-my.sharepoint.com/:v:/r/personal/jeff_brondell_snhu_edu/Documents/Code%20Review/Video%201.mov?csf=1&web=1&e=rOG0xf)

###### [Back to Top](#jeff-as-a-programmer)
## Software Design and Engineering

 This section is designed to show a level of comfort and proficiency with utilizing both basic and more complex coding practices. For this particular artifact you will first see that a new reporting page had to be designed and built. In order to display our Inventory history, we need a database connection, which we will explore later. The database will provide us with a historical list of items that have been added, altered, or removed from our Inventory application. This reporting screen will display that list and provide detailed information about the history. The storage and retrieval of data will be covered in a later section, but here you will see the work that goes into displaying that data in an efficient manner that allows users to easily understand the history of transactions. Working through this change provided a great chance for me to explore multiple options in how to design and display data on a screen. This is the area of this artifact that ties together the data storage aspects and the data logic, and the application of this can be universally applied to almost any program or design.

 Here we see the method created that allows the list of history_list objects to load and expand/contract as a table object on the activity. This code establishes a coded approach to building a table programmatically. We will pass our history_list object to this method, which is our list of all items stored on the history DB. This list will be traversed element by element as a way to build each row of the reporting table. 


 ```java
 
       //method that loads the list and creates the data table. creates format and aligns data to design of table.
    public void loadList(List<History> history_list){
        
        TableLayout report= (TableLayout) findViewById(R.id.historyTable);
        report.setStretchAllColumns(true);
        report.bringToFront();
        report.removeAllViews();

        //for each object on our history_list, we will create a new row and push data into the appropriate columns as determined below.
        for (int i = 0; i < history_list.size(); i++) {
            TableRow tr = new TableRow(getApplicationContext());
            TextView nameColumn = new TextView(getApplicationContext());
            nameColumn.setText(history_list.get(i).getItemName());
            TextView changeColumn = new TextView(getApplicationContext());
            changeColumn.setText(String.valueOf(history_list.get(i).getCountChange()));
            TextView typeColumn = new TextView(getApplicationContext());
            typeColumn.setText(history_list.get(i).getChangeType());
            TextView dateColumn = new TextView(getApplicationContext());
            dateColumn.setText(String.valueOf(format.format(history_list.get(i).getChangeDate())));
            TextView empty = new TextView(getApplicationContext());
            tr.addView(empty);
            tr.addView(nameColumn);
            tr.addView(changeColumn);
            tr.addView(typeColumn);
            tr.addView(dateColumn);


            report.addView(tr);
        }
    }
   ```
 
 
   This XML code is how the program determines not only how the table is displayed, but by utilizing the "Android:ID" tag, we get to identify the specific element to display from the Java coded activity. The TableLayout allows us to align the table with the page we've built here with the "wrap_content" setting. 
You'll also notice the ScrollView used here, which determines the size of the scroll area as well as the provide instructions on what section of our XML layout should be scrollable. Here we use this almost like a wrapper around our table so that the results can be scrolled, depending on the length of the reporting list.  
 ```xml

    <ScrollView
        android:layout_width="wrap_content"
        android:layout_height="match_parent"
        android:layout_columnSpan="6"
        app:layout_constraintTop_toBottomOf="@+id/nameSort"
        app:layout_constraintBottom_toBottomOf="parent">

        <TableLayout
         android:layout_width="wrap_content"
         android:layout_height="wrap_content"
         android:id="@+id/historyTable"
         >

        </TableLayout>

    </ScrollView>
 
 ```


 Here we see the final result of the list created for and presented on the Reporting page. We can see here that our list is fully formed and organized by the appropriate column headers and each row is aligned with the correct data. The buttons at the top act as headers as well as sorting options, which will be covered in our next section...
 
 ![Screen Shot 2021-12-08 at 4 18 37 PM](https://user-images.githubusercontent.com/61640483/145293722-b40e7f7c-b5cc-4353-beeb-07612cd6e350.png)


###### [Back to Top](#jeff-as-a-programmer)
## Data Structures and Algorithms

 A great deal of power in programming comes from our ability to create and manipulate data in organized and creative ways. To handle information programmatically we need to be able to structure data and access or modify it as our application requirements dictate. For this section we'll see the use of Algorithms and Data Structure that allow the inventory application to store and sort information dependent on the user's actions. This section is extremely important since working with data covers the vast majority of effort that goes into designing and programming an application. As we move through this section, we will see the sorting algorithms I've used to help sort data after it has been displayed. This "sorting" will essentially rely on our understanding of data and the position it holds within a structure. 

 Working through the following algorithms, although somewhat simple by data structure standards, has still provided me with a great working example of how to work with data through more complex methods. Being able to abstractly view information as a series of elements provides a great new opportunity for us to work with those elements. The following algorithms take advantage of these new opportunities by comparing elements, swapping elements, and evaluating them. The end result here will be a sorted list, but I will be able to apply these principles in many different ways in my future career fields. 

 Below we will see the code of the bubbleSort() method I created to sort the history_list object we've been provided in the earlier example. This method will traverse the list and compare each element to the subsequent element. Depending on the outcome of that comparison, the elements may be "Swapped" or switched, which is the primary mechanism that allows the list to be sorted. A bubble sort is a simple method in that it only uses two "loops" to work its way through a list of items, and swapping items only requires that on item be held temporarily until it can be placed in the appropriate location. While a bubble sort is not nearly the fastest option, its simplicity was a great companion for sorting our smaller list of items in the Inventory app. 

 As you review this code you may notice two separate comparisons, one for the "countChange", which represents the size of the inventory change. The second comparison included below is between elements "Id", which is the primary key from the database applied with each change. This "Id" essentially acts as a transaction counter, and is being used here to help order our bubble sort result by not only the change amount, but also by how recently they occurred.
 
```java
public void bubbleSort(List<History> list, String button){
            int n = list.size();
             for (int i = 0; i < n-1; i++){
                 for (int j = 0; j < n-i-1; j++){

                     if(button == "COUNT"){
                         if(list.get(j).getCountChange() > list.get(j + 1).getCountChange()) {
                             if(list.get(j).getId() < list.get(j + 1).getId()) {
                                 //swaping J and J+1
                                 History temp = list.get(j);
                                 list.set(j, list.get(j + 1));
                                 list.set(j + 1, temp);
                             }
                         }
                     }

```

 Here is a working example of a user accessing the reports page and then selecting each of the possible sorting options to reorganize the list to their specifications. More complex data or longer lists may benefit from the use of more complex algorithms, but the small size of this application allowed us to use one of the more basic options. As mentioned earlier, each of the buttons acts as a sorting option as well as a header for the list. We will spend time exploring how the data is housed and accessed in the next section...
 
![ReportsSorting](https://user-images.githubusercontent.com/61640483/144323938-4564e83c-3bd9-4ada-b601-683a6aea66fd.gif)

###### [Back to Top](#jeff-as-a-programmer)
## Database

 Many applications and programs are based around a fairly simple problem or question, which is "how do I manage the data and information". This question can have multiple complex answers, but at its core we're wondering how do we store data, how will we access data, and what will we do to that data once we have it. Using a database is generally a solid approach that helps us answer the first two questions. For this application we've stored our data in the form of "transaction history" in a separate SQL database. As you'll see, we're able to interact with and access this data through the use of an Android Studio open library option called the "Room Persistence Library".
 
 The Room Persistence Library has been used within the Inventory Application to allow the use of basic SQL database functions to store and manage historical data. The use of this library requires three different classes to be created and maintained. The "Entity" acts as the model and basic structure of the database table, the "Database" creates the table and links its creation to the "Entity, and the "DAO" allows us to create SQL like commands to be executed within Java code that control interaction with data in the database. 
 
 Working with data in this method allows me to showcase my own proficiency in a commonly required skill set with potential employers. However, I'd also like to note that my experience in this final project has helped to solidify those skills into a more well-rounded and working set that I can use in the future. The creation of the History database and its many components required a level of planning that I had yet to put into practice. Designing the application around our use and reliance on this database also helped to improve my understanding for approaches and considerations that should be made when programming an application. For example; we need to consider data security when we design how a user will interact with data that is linked to a database. If a user is provided with methods that allow them to input data in a way that can then be sent to our database without protection, it is possible for them to "high-jack" our application. With that in mind, each data element in this application is strongly typed and closely controlled. These protections will ensure that we maintain control over the application and data and not the user. 

 The entity object, as annotated here, acts as the model of the database object. It determines the fields of both the database and the objects that will be used to fill that database.  You will notice below that each field has annotations that help describe how that field should be viewed within the database.  For example; you will notice the "Id" field is noted as the "PrimaryKey", which enables each history entry to be viewed as a separate entry into the database. 
### Entity
```java
//Entity object acts like a model of the database/history object/entities. Each field represents a  column in the database.
// annotations are used to establish characteristics of each field.
@Entity(tableName = "History")
@TypeConverters(DateConverter.class)
public class History implements Serializable {


      @NonNull
      @PrimaryKey
      @ColumnInfo(name="id", defaultValue = "0")
      private Integer id;

        @NonNull
        @ColumnInfo(name="itemName")
        private String itemName;

        @NonNull
        @ColumnInfo(name="countChange")
        private int countChange;

        @ColumnInfo(name="changeType")
        private String changeType;

        @ColumnInfo(name="changeDate")
        private Date changeDate;

        public History() {
        }
```
 The database file simply acts as a summary of the elements that will make up our database. We establish the Name of our DB, as well as the Entity Class to determine how that DB is build and the DAO class that determines how we interact with that DB. Here you will see a class that establishes all three critical elements of our database. 
### Database
```java

//Database class initializes database and determines dao to use.
@Database(entities ={History.class},version = 1)
public abstract class HistoryDatabase extends RoomDatabase {
    private static final String DATABASE_NAME = "history3.db";

    private static HistoryDatabase historyDatabase;

    public abstract HistoryDao historyDao();
}
```

 The DAO class acts as a class that determines the ways in which we can engage with data on our database. Each method is annotated in a way that tells the application how we plan to use it. For example, the getHistory() method is listed as a "Query", and it is designed to retrieve all of the information from the History database and return a list or History objects to the application. We will use this list, as shown in the previous sections, to sort and display our Inventory history data. 
### DAO
```java

//DAO (data access object) class allows a user to interact with the database via use of the provided/defined methods
@Dao
public interface HistoryDao {

    @Query("SELECT * FROM History")
    public List<History> getHistory();

    @Query("SELECT MAX(id) FROM History")
    public int getMaxId();

    @Query("SELECT * FROM History WHERE itemName= :itemName")
    public List<History> getHistoryByItemName(String itemName);

    @Insert(onConflict = OnConflictStrategy.ABORT)
    public void insertHistory(History history);

    @Update
    public void updateHistory(History history);

    @Delete
    public void deleteHistory(History history);

}
```

With Database created and running, we are now able to interact with data stored within it. For example; below shows how we update the history each time an item is added to the Inventory list. This updateHistory() method pulls the current maxId, increments it by one, and sets each attribute of the history object based on the change being made. This history object is then inserted into the database via the use of the previously created HistoryDAO class. 

```java
public void updateHistory(View view){
        try {
            maxId = historyDao.getMaxId();
        }
        catch (IllegalStateException e) {
            maxId = 0;
        }

        Date date = java.util.Calendar.getInstance().getTime();
        int changeAmt = itemAdd.getItemCount();

        history.setId(maxId + 1);
        history.setItemName(itemAdd.getItemName().toString());
        history.setCountChange(changeAmt);
        history.setChangeType("CREATE");
        history.setChangeDate(date);

        historyDao.insertHistory(history);
    }

```
###### [Back to Top](#jeff-as-a-programmer)

#### For more context on this project:
Visit [My Inventory Application](https://github.com/Brondell01/InventoryApp.git)

#### You can view the starting point for this project:
Here [Inventory Pre-Enhancement](https://github.com/Brondell01/cs-360.git)
