## Welcome to Brondell01's GitHub Page

It's at this Point that I'll attempt to provide access to the Code Review of my initial Inventory Applicaton artifcat. The purpose of the code review was to indentify issues that needed correction and illustrate planned changes that would meet the requirements of the Capstone course final project. 

###### Lis of items to complete.
- [x]  create new functionality for reporting within application
- [x]  draw conclusions on how new ehnacments meet basic requirements for employement
- [x]  begin to develop IO page/explore functionality
- [x]  clean up code for readability
- [ ]  draft format and wording for showcase
- [ ]  finalize ePortfolio


--
As you explore this ePortfolio please recognize that it has been desigined with a purpose. The intent here is to provide a working example of my personal skill set combined with a professional level presentation. The following sections will first introduce you to who I am as a developer, and then move on into the skill based portions of this portfolio.

For this portfolio and it's different sections I've focused on updating an existing data artifact I had developed for one of my higher level SNHU courses. Throughout this page you will different enhancments I've made to a simple Inventory Application, which has been designed for an android mobile device. These enhancements will showcase skills in the areas of Software Design and Engineering, Algorithms and Data Structures, and finally Databases. The end result will hopefully show you not only a proficeincy withtin these targeted areas, but also a more robust and professional approach to developing skills necessary for any role within the industry. 

## Jeff as a Programmer
Throughout my time at SNHU I've had plenty of opportunties to produce code and develop applications. Each of my assignments was initially developed with a "pass this class" mentality. However, given more time, I've had a chance to relfect on my exprience and hone in on who I am as a developer and how my skills fit within the program as it's been defined. This is where we discuss how I approach and solve problems, as well as apply focus on the more specific skill set I bring to the role of software developer. 

As this ePortfolio will show, I have more than a competent level of skill when it comes to working with code and the different nuanced approaches that are required to get it to function.  First among all considerations is "does it work?", following this question any developer will understand and appreciate the numerous ways that any problem can be solved. As I've worked through SNHU and more specifically, through this course, i've come to recognize central tenants of my approach that aid in my success. 

I've learned that a formulatic approach helps to solve any problem, and that this view is essential to developing a working code base. At its core, developing code is essentially a codified response to a problem. We are trained and presented with tools, and are then asked to apply our knowledge and expeirence in a way that best solves a given requirement. My strength as a programmer comes from that process and the steps in which a problem is defined and broken down and then solved. 

you will see in the following sections that each "problem" has a different solution. The culmination of thise solutions will represent a fully functional application. As you view this portfolio please focus on the skill areas of focus, as these areas were intentionallly over developed to highlight skills and solutions. 

#### Areas of Focus.
- Software Design and Enineering
- Data Structures and Algorithms
- Databases

## Code Review
For this artifact I've taken the time to run through a formal code review process of the Inventory Applicaton. As stated, this application provides a great opportunity to showcase various skills. The code review here will set a functional baseline for the artifact as it stood prior to this course. It's important to remember that this artifact was created for a previous course and the planned enhancements I discuss in the review will not only improve the existing code base but expand it's functionality to match the project requirements. 

As you will see in the following videos, a review of the code provides a great opportunity to identify potential improvments and gaps in logic, as well as refocusing attention on some of the smaller details associated with creating an application. As this Inventory Application currently stands, you will see a great deal of redundant code and a general lack of clairty in design. The code review video will walk you through my thought process as I identify needed improvements and plan my next steps. 

For viewing the Code Review see [Selected Artifact initial code review](https://snhu-my.sharepoint.com/personal/jeff_brondell_snhu_edu/_layouts/15/onedrive.aspx?id=%2Fpersonal%2Fjeff%5Fbrondell%5Fsnhu%5Fedu%2FDocuments%2FCode%20Review), or start by viewing the following video. 

[![This is an image](https://user-images.githubusercontent.com/61640483/144322045-40b010b1-8696-4cdf-b4db-8f92b1c2648d.png)](https://snhu-my.sharepoint.com/:v:/r/personal/jeff_brondell_snhu_edu/Documents/Code%20Review/Video%201.mov?csf=1&web=1&e=rOG0xf)

<details><summary>## Software Design and Engineering</summary>
<p>

This section is designed to show a level of comfort and proficiency with utilizing both basic and more complex coding practices. For this particular artifact you will first see that a new reporting page had to be designed and built. In order to display our Inventory history we need a database connection, which we will explore later. The database will provide us with a historical list of items that have been added, altered, or removed from our Inventory application. This reporting screen will display that list and provide detailed information about the history. The storage and retrevial of data will be covered in a later section, but here you will see the work that goes into displaying that data in an efficient manner that allows users to easily understand the history of transactions.

Here we see the method created that allows the list of history_list objects to load and expand/contract as a table object on the activity. This code establishes a coded approach to building a table programatically. We will pass our history_list object to this method, which is our list of all items stored on the history DB. This list will be traveresed element by element as a way to build each row of the reporting table. 

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

</p>
</details>
## Algorithms and Data Structures

Section will be used to highlight the code and explain the functionality of the sorting added to the report feature.  For example; let's include and describe the bubble sort here....
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

here we will show the quicksort algorithm, but it should be noted that this is not used in the code. 

Quick sort intitial algorithm which compares elements as it moves from the middle of the elements.
```java
public void quickSortChange(int lowerIndex, int higherIndex){
        int i = lowerIndex;
        int j = higherIndex;
        int pivotInt = lowerIndex + (higherIndex - lowerIndex)/2;

        int pivot = sort_list.get(pivotInt).getCountChange();

        while( i <= j) {
            while (sort_list.get(i).getCountChange() < pivot){
                i++;
            }

            while (sort_list.get(j).getCountChange() > pivot){
                j--;
            }

            if(i <= j) {
                switchItems(i, j);
                i++;
                j--;
            }
        }
        //call quicksort recursively
        if (lowerIndex < j){
            quickSortChange(lowerIndex, j);
        }
        if (i < higherIndex){
            quickSortChange(i, higherIndex);
        }
    }
```

SwitchItems() method called by the QuickSorth() algorithm to swap elements in a list. Only called when necessary by QuickSorth().
```java

 public void switchItems(int i, int j){
        History temp = sort_list.get(i);
        sort_list.set(i,sort_list.get(j));
        sort_list.set(j,temp);
        }
```

## Database

The Room Persistence Library has been used within the Inventory Application to allow the use of basic SQL database functions to store and manage historical data. The use of this library requires three different classes to be created and maintained. The "Entity" acts as the model and basic structure of the database table, the "Database" creates the table and links it's creation to the "Entity, and the "DAO" allows us to create SQL like commands to be executed within Java code that control interaction with data in the database. 

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
### Reporting page  gif

for use later in development of page, can use this screen shot to illustrate reports page and sorting functions. 

![ReportsSorting](https://user-images.githubusercontent.com/61640483/144323938-4564e83c-3bd9-4ada-b601-683a6aea66fd.gif)




### Beyond this point You'll find instructions that I'll eventually delete. 

You can use the [editor on GitHub](https://github.com/Brondell01/Brondell01.github.io/edit/main/README.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/Brondell01/Brondell01.github.io/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
