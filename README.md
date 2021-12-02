## Welcome to Brondell01's GitHub Page

It's at this Point that I'll attempt to provide access to the Code Review of my initial Inventory Applicaton artifcat. The purpose of the code review was to indentify issues that needed correction and illustrate planned changes that would meet the requirements of the Capstone course final project. 

For viewing the Code Review see [Selected Artifact initial code review](https://snhu-my.sharepoint.com/personal/jeff_brondell_snhu_edu/_layouts/15/onedrive.aspx?id=%2Fpersonal%2Fjeff%5Fbrondell%5Fsnhu%5Fedu%2FDocuments%2FCode%20Review).

[![This is an image](https://user-images.githubusercontent.com/61640483/144322045-40b010b1-8696-4cdf-b4db-8f92b1c2648d.png)](https://snhu-my.sharepoint.com/:v:/r/personal/jeff_brondell_snhu_edu/Documents/Code%20Review/Video%201.mov?csf=1&web=1&e=rOG0xf)



###### Lis of items to complete.
- [x]  create new functionality for reporting within application
- [x]  draw conclusions on how new ehnacments meet basic requirements for employement
- [x]  begin to develop IO page/explore functionality
- [ ]  clean up code for readability
- [ ]  draft format and wording for showcase
- [ ]  finalize ePortfolio

### Reporting page  gif

for use later in development of page, can use this screen shot to illustrate reports page and sorting functions. 

![ReportsSorting](https://user-images.githubusercontent.com/61640483/144323938-4564e83c-3bd9-4ada-b601-683a6aea66fd.gif)




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


## Database

Section will be used to highlight the code and explain the functionality of the history Database.

###Entity
```java

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

```


###DAO
```java
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
