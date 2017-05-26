## Welcome to Vanessa's Recipe Book!

My recipeBoook will allow the users to store all of their all-time favourite recipes into a digital book, the code and images are presented below. 

<img src= "file:///Users/vanessamm/Desktop/UML%20Diagram.png"/>
![Image](src)

### Code

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
#  INTERFACE 
public interface Recipe
{
    public String recipeDetail(); 
}

#  ABSTRACT CLASS
public abstract class RecipeStructure 
{
    String course, recipeName;
    double prepTime, cookingTime;
    int numOfIngredients, servings, recipeNameLength; 
    boolean startFromBeginning;//identify all instances
    abstract void setRecipeName(String Recipe);
    abstract String getRecipeName();
    abstract void setCourse(String course);
    abstract String getCourse();
    abstract void setPgNum(int pg);
    abstract int getPg();
    abstract void setNumOfIngredients(int numOfIngredients);
    abstract int getNumOfIngredients();
    abstract void setServings(int servings);
    abstract int getServings();
    abstract void setPrepTime(double prep);
    abstract double getPrepTime();
    abstract void setCookingTime(double cook);
    abstract double getCookingTime();
    abstract void startFromBeginning(boolean beginning);
    abstract boolean getStartFromBeginning();
    abstract double totalTime();
    abstract double pgNum();
    abstract double pgNum(double minPgNum);
    abstract int recipeNameLength();
}//end abstract class

#  RECIPEBOOK 
public class RecipeBook extends RecipeStructure implements Recipe

{
    private String course; //ex. appetizer, dessert
    private String recipeName;
    private int pgNum;
    private int numOfIngredients;
    private int servings;
    private int recipeNameLength;
    private double prepTime;//in hours
    private double cookingTime;//in hours
    private boolean startFromBeginning;
    //initialize varaibles 
    
    public RecipeBook()
    {
       course= "Main Course";
       recipeName="Mint Peas and Pancetta Risotto";
       servings=8;
       prepTime=1.0;
       cookingTime=1.0;
       numOfIngredients=6;
    }//end zero-arg constructor
     public RecipeBook(String course, String recipe, int servings, double prep, double cook, int numOfIngredients)
    {
       this.course= course;
       this.recipeName=recipe;
       this.servings=servings;
       this.prepTime=prep;
       this.cookingTime=cook;
       this.numOfIngredients=numOfIngredients;
    }//end multi-arg constructor
    
    public void setRecipeName(String recipe)
    {
        this.recipeName=recipe; 
    }
     public String getRecipeName()
    {
        String recipe=recipeName.substring(1,recipeName.length());
        recipeName= recipeName.substring(0,1).toUpperCase();
        recipeName+=recipe;
        return recipeName;
    }//changes the first letter of recipe name to uppercase
    
    public void setCourse(String course)
    {
        this.course=course;
    }
    public String getCourse()
    {
        course=course.substring(0,course.length());//substring method
        course=course.toUpperCase();//converting to upper case
        return course;
    }
    
    public void setPgNum(int pg)
    {
        this.pgNum=pg;
    }
    public int getPg()
    {
        return pgNum;
    }
    
    public void setNumOfIngredients(int numOfIngredients)
    {
        this.numOfIngredients= numOfIngredients;
    }
    public int getNumOfIngredients()
    {
        return numOfIngredients;
    }
    
    public void setServings(int servings)
    {
        this.servings=servings;
    }
    public int getServings()
    {
        return servings;
    }
    
    public void setPrepTime(double prep)
    {
        this.prepTime= prep;
    }
    public double getPrepTime()
    {
        return prepTime;
    }
    
    public void setCookingTime(double cook)
    {
        this.cookingTime=cook;
    }public double getCookingTime()
    {
        return cookingTime;
    }
    
    public void startFromBeginning(boolean beginning)
    {
        this.startFromBeginning=beginning;
    }
    public boolean getStartFromBeginning()
    {
        return startFromBeginning;
    }
    //setter and getter for all variables
    public double totalTime()
    {
        double totalTime= prepTime + cookingTime;
        return totalTime; 
    }//calculates total time by adding prep and cooking time
    public double pgNum()
    {
        pgNum= (int)(Math.random()*20)+1;//casting 
        return pgNum;
    }//flip to random page of the recipe book
    public double pgNum(double minPgNum)//overloaded method
    {
        minPgNum=1;
        if (getStartFromBeginning()==(true))
        {
          minPgNum=1;
        }
        return minPgNum;
    }//flip to first page of the recipe book
    public int recipeNameLength()
    {
        recipeNameLength= recipeName.length();//string method to find length of string
        return recipeNameLength;
    }//determines the length of the recipe string
    public String recipeDetail()
    {
        String output= new String();
        output= "pg."+ pgNum() + "\nCourse:" + getCourse() + "\nRecipe Name:" + getRecipeName() + 
        "\nServings:" + servings + "\nTotal Cook Time:" + totalTime() + "hrs    Prep Time:" 
        + prepTime + "hrs    Cooking Time:" + cookingTime + "hrs\n";
        return output; 
    }//implements method from interface
    public String toString()
    {
        return recipeDetail();
    }//end toString() method
}//ends main class

#  RECIPEBOOK DRIVER 
import java.util.Scanner;//import package for Scanner
public class RecipeBookDriver
{
    public static void main (String[] args)
    {
        Scanner RecipeBook= new Scanner (System.in);
        RecipeStructure recipe1= new RecipeBook();//POLYMORPHISM
        System.out.println("Please enter the course of the recipe it belongs to: ");
        recipe1.setCourse(RecipeBook.nextLine());
        System.out.println("Please enter the name of the recipe: ");
        recipe1.setRecipeName(RecipeBook.nextLine());
        System.out.println("Please enter the number of servings the recipe will yield: ");
        recipe1.setServings(RecipeBook.nextInt());
        System.out.println("Please enter the number of hours the preparation will take: ");
        recipe1.setPrepTime(RecipeBook.nextDouble());
        System.out.println("Please enter the number of hours the cooking process will take: ");
        recipe1.setCookingTime(RecipeBook.nextDouble());
        System.out.println("Please enter the number of ingredients needed for the recipe: ");
        recipe1.setNumOfIngredients(RecipeBook.nextInt());
        //sets all variables for recipe1
        RecipeStructure recipe2= new RecipeBook();//POLYMORPHISM
        while (recipe2.getNumOfIngredients()<=4 || recipe2.totalTime()<=0.5)
        {
            System.out.println("\nDifficultly: Beginner");
        }//determines difficulty of recipe 2 through while loop 
        do
        {
            System.out.println("\nDifficulty: Medium/Home Cooks");
            break;
        }
        while (recipe2.getNumOfIngredients()>4 && recipe2.getNumOfIngredients()<=10);
        //determines difficulty of recipe 2 through do while loop 
        if (recipe2.getNumOfIngredients()>10)
        {
            System.out.println("\nDifficulty: Professional");
        }//detemines difficulty of recipe 2 through if-statement
        System.out.println(recipe2);//prints recipe2 (from zero-arg constructor)
        if (recipe1.getNumOfIngredients()<=4 || recipe1.totalTime()<=0.5)
        {
            System.out.println("Difficultly: Beginner");
        }
        else if (recipe1.getNumOfIngredients()>4 && recipe1.getNumOfIngredients()<=10)
        {
            System.out.println("Difficulty: Medium/Home Cooks");
        }
        else 
        {
            System.out.println("Difficulty: Professional");
        }//detemines difficulty of recipe 1
        System.out.println(recipe1);//prints recipe1 (decided by user)
        switch (recipe1.getCourse())
        {
            case"DESSERT":
            System.out.print("Try using sugar substitutes such as honey, vanilla, or agave nectar." +
            "\nPlease adjust the sugar level to your own liking/preference.\n");
            break;
        }//healthy alternate suggestion for sugar 
        if (recipe1.getPrepTime()<=0 || recipe1.getCookingTime()<=0)
        {
            throw new IllegalArgumentException("Error. Prep or cooking time cannot be less than or equal to 0.");
        }//prep and cooking cannot be less than 0 hr
        else
        {
            System.out.print("Happy cooking and");
        }
        if (recipe1.getServings()<=0)
        {
            throw new IllegalArgumentException("Error. Serving cannot be less than or equal to 0.");
        }//servings cannot be less than 0 
        else 
        {
            System.out.print(" Bon Appetite!");
        }
    }//ends main method
}//ends main class



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

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/vanessamm922/vanessamm922.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
