Download Link: https://assignmentchef.com/product/solved-adv-lab-5-scala-functional-programming-techniques
<br>
In this lab you will gain further practice in functional programming in Scala and learn how to create a simple menu-driven application in Scala. You will work with <u>partial function application</u> and <u>currying</u>, and see examples of the use of <em>map</em>, <em>flatMap</em> and <u>for comprehensions</u>.

For this lab you should create an IntelliJ Scala project <em>lab5project</em>. Tasks 1 and 2 can be done with Scala worksheets, while Task 3 will require you to create a Scala application in your project.

Task 1. Partial function application and currying

<strong>Example 1 – Partially applied function</strong>

<ol>

 <li>Define and test a function <em>isDivisible</em> which has two integer parameters x and y and returns true if x is divisible by y, false otherwise.</li>

 <li>Define a variable <em>isEven</em> and assign to it the result of partially applying <em>isDivisible</em> as follows:</li>

</ol>

val isEven = isDivisible(_: Int, 2)

What is the type of <em>isEven</em>?

<ol start="3">

 <li>Test that you can apply <em>isEven</em> to a single parameter and check whether it is even, for example</li>

</ol>

isEven(10)

<ol start="4">

 <li>Use <em>isEven</em> as a predicate in the filter method of List to transform List(1,2,3,4,5,6,7,8,9,10) to a list containing even numbers only.</li>

</ol>

<strong>Example 2 – Another partially applied function</strong>

In lab 4 you worked with a map containing airport cities and codes. In this example you will create functions to iterate through and print the contents of a similar map.

<ol>

 <li>Create the following map:</li>

</ol>

var airports = Map(“Glasgow” -&gt; “GLA”, “Dubai” -&gt; “DXB”, “Berlin” -&gt; “TXL”)




<ol start="2">

 <li>Define and test the following function to print the keys and values in a map:</li>

</ol>

def printMap(mymap: Map[String,String]) = {for ((k, v) &lt;- mymap) {println(s”$k – $v”)}}

<em>Note that this function will work only for a map where keys and values are strings. A more generic version of the function that could be used with other types for keys and values could be defined:</em>




<em>def printMap[A,B](mymap: Map[A,B]) = {for ((k, v) &lt;- mymap) {println(s”$k – $v”)}}</em>

<em>However, for this exercise it will be simpler to use the first version and work with strings only,</em> <em>although if you prefer you can use the generic approach.</em>

<ol start="3">

 <li>Modify <em>printMap</em> as follows so that it becomes a higher-order function, where the second parameter is a function that determines how to print each key-value pair.</li>

</ol>

def printMap(mymap: Map[String,String],f:(String,String)=&gt; Unit) = {for ((k, v) &lt;- mymap) {f(k,v)}}




Don’t try to test the modified <em>printMap</em> yet. In the following steps you will define functions that can be used for the second parameter of <em>printMap</em>, and then you will test it.

<ol start="4">

 <li>Define the following function that can be used as a parameter – this function prints a key and value in the same format as the first version of <em>printMap</em>.</li>

</ol>

def printKeyValue(k:String, v:String) = {println(s”$k – $v”)}

<ol start="5">

 <li>Define a similar function <em>printValueOnly</em> that prints out a value only in the following format:</li>

</ol>

Value – GLA

<ol start="6">

 <li>Test the higher-order <em>printMap</em> function using the airports map and each of the functions <em>printKeyValue</em> and <em>printValueOnly</em></li>

 <li>Define a variable <em>printKeysValues</em> and assign to it the result of partially applying <em>printMap</em>, specifying the function parameter only, as <em>printKeyValue</em>. The type of <em>printKeysValues</em> should be Map[String,String] =&gt; Unit.</li>

</ol>

Test as follows:

printKeysValues(airports)

Note that if you were frequently needing to print out the keys and values of maps in an application, your code could be made simpler and more readable using this technique.

<strong>Example 3 – Curried function</strong>

<ol>

 <li>Create a <u>curried</u> version of <em>printMap</em>, called <em>printMap_curried</em>. This will involve simply modifying the parameter list. You should be able to test your curried function by calling it as follows:</li>

</ol>

printMap_curried(airports)(printValueOnly)

<ol start="2">

 <li>Test also by calling the curried function with a lambda expression as the second parameter list, and enclosing this in {} instead of () as follows:</li>

</ol>

printMap_curried(airports){(k,v)=&gt; println(s”Key –  $k”)}

<ol start="3">

 <li>How would this compare with calling <em>printMap</em> with a lambda? Which would be clearer and more readable?</li>

</ol>

<h3>Task 2. Map, flatMap and for comprehensions</h3>

<strong>Example 1 – Comparing map and flatMap</strong>

In this task you will extract data from Scala maps using <em>map</em> and <em>flatMap</em>,  and you will see how the same results can be achieved, more conveniently, using <u>for comprehensions</u>.




<ol>

 <li>Create the following map as your data for this exercise (or continue from Task 1):</li>

</ol>




var airports = Map(“Glasgow” -&gt; “GLA”,“Dubai” -&gt; “DXB”,“Berlin” -&gt; “TXL”)




<ol start="2">

 <li>Use the <em>get</em> method of Map to find the value (airport code) for a given key (city)?</li>

</ol>




airports.get(“Glasgow”)




<ol start="3">

 <li>Try doing the same for a key that doesn’t exist in the map:</li>

</ol>

airports.get(“Edinburgh”)




What values did you get? What is the type of the result returned by get?




<ol start="4">

 <li>Now you will search in the <em>airports</em> data for the airport codes for all cities in a list. Create the search list as follows:</li>

</ol>




var searchlist = List(“Glasgow”, “Edinburgh”, “Berlin”)




Note that the search list includes Edinburgh, which is not included in the data. How do you think you would approach this problem using an imperative approach? In Scala, it’s a one-liner. Enter the following code:




val codes = searchlist.map(x =&gt; airports.get(x))




Describe the contents of the variable <em>codes</em>. This code takes each element of <em>searchlist</em> and maps it to the value matching the key equal to that element in the <em>airports</em> data.




<ol start="5">

 <li>Modify the expression for <em>codes</em> to use <em>flatMap</em> instead of <em>map</em>, and describe the difference this makes to the result.</li>

</ol>






















<strong>Example 2 – <em>for</em> expression</strong>




<ol>

 <li>The following expression is equivalent to the expression you used in example 1. Test this expression to check that it gives the same result as in step 5 of example 1.</li>

</ol>




val codes_for = for{x &lt;- searchlisty &lt;- airports.get(x)} yield(y)




This example uses a <u>for comprehension</u>. For comprehensions can be thought of as “syntactic sugar” for <em>map/flatMap</em>, and are often easier to write and understand. <em>x</em> and <em>y</em> are known as <u>generators</u>. Note that the y generator includes a reference to <em>x</em>, and this is equivalent to the <em>flatMap</em> call above. The yield expression allows you to define what result is returned from the generators.







<strong>Example 3 – Chaining functions</strong>




In example 1 you obtained a list of airport codes for the airports data based on a list of search values. Now you will apply a further transformation to the result extracted from the data by converting all the codes to lower case




<ol>

 <li>Enter the following code, which applies the function <em>toLowerCase</em> to each element in the result of the search.</li>

</ol>




val codes_lower = searchlist.map(x =&gt;airports.get(x)).map(y=&gt;y.toLowerCase)




What happens? Why can you not apply <em>toLowerCase</em>?




<ol start="2">

 <li>Modify the expression for <em>codes_lower</em> to use <em>flatMap</em> instead of <em>map</em>, and describe the difference this makes. Why does the use of <em>flatMap</em> allow these transformations to be chained?</li>

</ol>




<ol start="3">

 <li>Write an equivalent for expression to achieve the same result. This will involve changing only the yield expression in example 2.</li>

</ol>







<strong>Example 4 – A more complex for comprehension</strong>




The final example is a bit more complicated, to demonstrate more of the power of for comprehensions. You will define the search using the keys of a map rather than a list, and you will combine the values in the search map with the values extracted from the data.




<ol start="4">

 <li>Create the following map:</li>

</ol>




var searchmap = Map(“Glasgow” -&gt; “Scotland”,“Edinburgh” -&gt; “Scotland”,“Berlin” -&gt; “Germany”)




The aim of this exercise is to find the airports, if any, matching the keys in these map, and for each result found, combine the code with the matching country name in the search map, to get the result:




List(GLA – Scotland, TXL – Germany)




<ol start="5">

 <li>Enter the following code and check that it gives the required result. Study the code (and the comments) to make sure you understand how it works. Why do you need the final call to <em>.toList</em>?</li>

</ol>




val codes_countries_for =  for{x &lt;- searchmap.keys    // the keys in the searchmapy &lt;- airports.get(x)   // get codes for which a value existsz &lt;- searchmap.get(x)  // country for each key in searchmap} yield(y + ” – ” + z)

codes_countries_for.toList




<ol start="6">

 <li>Note that this could also be written using <em>map/flatMap</em> calls, but this one is definitely easier with a for comprehension.</li>

</ol>




For comprehensions are very powerful and there are many possible variations to solve a wide range of problems. There are more examples in your lecture notes, and you can find some more useful examples at:




https://gist.github.com/loicdescotte/4044169http://eddmann.com/posts/using-for-comprehensions-in-scala/










<h3>Task 3. Creating a (functional) menu-driven application</h3>




Scala can be used to build pretty much any type of application, for example GUI applications (using Java UI libraries) or web applications (using a framework such as Play). In this task, though, you will create a simple text-based menu-driven console application. You may have created applications like this using other languages, but this example will have a functional twist or two.




The application will read in some data from a text file which contains Bundesliga football teams and their current points total. This data will be stored in a Map. Here is an excerpt from the file:




Bayern Munich, 24RB Leipzig, 24Hoffenheim, 20

The application will then display a menu with options to extract and process information from the data. Actually there will only two options initially, to list the teams and their points in order of the number of points, and to quit the application. An example session (with some output omitted for brevity) is shown below:




Please select one of the following:

1 – show points for all teams

2 – quit

1

Bayern Munich: 24

RB Leipzig: 24

Hertha BSC: 20

…

Please select one of the following:

1 – show points for all teams

2 – quit

2

selected quit




Process finished with exit code 0




Most of the code for the application will be provided for you – you will create the application and add this code to it. This will provide an example which will help you with your coursework.




<ol>

 <li>Download the file <em>zip</em> and extract its contents, a set of .txt files. Open <em>data.txt</em> in an editor and observe the contents.</li>

</ol>




<ol start="2">

 <li>Create a new Scala object called MyApp in the src folder in your project. Remember that to do this you right-click on the folder and select New &gt; Scala class from the menu. In the Create New Scala Class dialog, enter the name and select Object for Kind.</li>

</ol>




<ol start="3">

 <li>Add the following imports at the top of MyApp.scala:</li>

</ol>




import scala.io.Sourceimport scala.io.StdIn.readInt

import scala.io.StdIn.readLineimport scala.collection.immutable.ListMap




<ol start="4">

 <li>Make object MyApp extend App.</li>

</ol>




<strong>Reading the data from file</strong>




<ol>

 <li>Copy the file <em>txt</em> into the root folder of your project.</li>

</ol>




<ol start="2">

 <li>Add the contents of the file <em>txt</em> into MyApp, inside the object MyApp. Note that this code calls a function called <em>fileRead</em> and assigns the result to a variable <em>mapdata</em>. This variable is the data for the application, and is of type Map[String, Int]. The code also prints the data so that you can check that it has been read correctly.</li>

</ol>




<ol start="3">

 <li>Add the contents of the file <em>txt </em>into MyApp immediately after the existing content. This defines the <em>fileRead</em> function. Review the comments in the code to understand how it works.</li>

</ol>




<ol start="4">

 <li>Run the application (right-click on the object in the Project View and select Run). Check that the data is as you expect. Don’t worry about the order that the teams appear in the data, a Map in Scala is not sorted (if you want to have the items sorted by key you can use a SortedMap instead).</li>

</ol>




<ol start="5">

 <li>Once you are confident that the data is being read correctly you can remove or comment out the line that prints the data.</li>

</ol>




<strong>Creating the menu</strong>




<ol>

 <li>Add the contents of the file <em>txt</em> into MyApp, immediately after the code from <em>applogic_file.txt</em>. This code defines an action map, of menu options and the functions they map to, and calls functions to read user input and invoke corresponding functions. Review the comments in the code. The code will not compile at this point as there are references to functions that have not been defined yet.</li>

</ol>




<ol start="2">

 <li>Add the contents of the file <em>txt</em> after the existing code. This includes functions to:</li>

</ol>

<ul>

 <li>Show a menu (with two options) to the user and read the user’s selected option</li>

 <li>Invoke a function specified by the user input and the corresponding value in the action map</li>

 <li>Implement the actions referred to in the action map, to handle each of the menu options. Note that the handler for option 2 simply prints a message and returns false which will cause the application to terminate.</li>

</ul>

Review the comments in the code. Note that the function <em>mnuShowPoints</em> is a higher-order function, whose parameter is the operation that produces the data to be displayed. This code will still not compile as some functions have not been defined yet.




<strong>Creating the functionality for the menu options and running the application</strong>




<ol>

 <li>Add the contents of the file <em>txt</em> after the existing code. This defines a function to implement the “show points for all teams” menu option. If an option requires further user input then this function would get that input. This particular option doesn’t need any further user input, though, so just does the following:</li>

</ol>

<ul>

 <li>Applies the function that is passed to it as a parameter to get the data to display</li>

 <li>Iterates through the data and prints to the output</li>

</ul>




<ol start="2">

 <li>Add the contents of the file <em>txt</em> after the existing code. This defines a function to get the data for the “show points for all teams” menu option (it returns the full set of data in the original map, except sorted in descending order of points).</li>

</ol>




<ol start="3">

 <li>The code should now be complete. Run the application, and select option 1. You should see the teams and their points, with the team with the highest number of points first.</li>

</ol>




<ol start="4">

 <li>Select option 2. The application should terminate.</li>

</ol>




<strong>Adding a menu option</strong>




Add a menu option to show the points for a team chosen by the user.




You will need to modify the action map and functions that implement the menu, with a new option that calls




mnuShowPointsForTeam(currentPointsForTeam)




You will also need to add and complete the following functions:




def mnuShowPointsForTeam(f: (String) =&gt; (String, Int)) = {// needs to print a prompt and use readline to get user input

// should apply function f to user input string and print result

// note that the result of f is a tuple}




def currentPointsForTeam(team: String): (String, Int) = {// should retrieve points value from mapdata for key team and

// return a tuple of team and points

// remember that get returns an option so you will have to

// pattern match to get the value

}




Test your modified application. An example session would look like this:




Please select one of the following:

1 – show points for all teams

2 – show points for selected team

3 – quit

2

Team&gt;Hertha BSC

Hertha BSC: 20

Please select one of the following:

1 – show points for all teams

2 – show points for selected team

3 – quit

2

Team&gt;Liverpool

Liverpool: 0

Please select one of the following:

1 – show points for all teams

2 – show points for selected team

3 – quit




Note that in this implementation if a team name is entered that is not included in the data then the points is shown as 0.







<strong>Final note</strong>




Note that since Scala supports object-oriented programming, we could have used classes to organise the code, for example by making the menu action functions methods of a controller class. However, we are focusing on the functional programming techniques here so we simply put all functions within the MyApp object.