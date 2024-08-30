# SWITCH-function_with_charts
Wondering how to allow the report user to change the measure that is displayed on the chart?  
With help comes the SWITCH function !
-------------------------
For the purpose of the task, let's prepare a column chart -> stuck column chart.
Let's put the year on the X-axis,
on the Y-axis total sales,
in the hatch, let's put the brand category.

Result :

![image](https://github.com/user-attachments/assets/4576b6e5-06f1-4db2-ab8c-e57de73c847b)

To solve our task we need two things : 
1) a table containing a list of names to which we will assign measures. The table will consist of two columns “measure id” and “measure names”.
2) a measure with a SWITCH function

Let's create a new table !
On the HOME tab, in the DATA section, you will find “Enter data”.

![image](https://github.com/user-attachments/assets/c2ccddff-858b-4ae4-9f5d-4122f5dbec53)

Next, let's create a list of measures that we want to switch on the chart.

![image](https://github.com/user-attachments/assets/ad27359d-448e-46d9-9eca-27e8316e1390)

An important step is to sort the measure name column by ID. 
This will allow us to freely set the order of measure display.

To do this we click on the newly created table then on the “Measure Name” column we go to “Column tools” and in the Sort section we select Measure ID.

![image](https://github.com/user-attachments/assets/f5f1411d-e91c-480d-b12c-19d399a1ce5a)

Great !
Now all that's left is to create a measure and add a slicer !
----------------------------------------
This DAX measure is used in Power BI and leverages the SWITCH function to dynamically select and display different measures based on the value selected by the user. Below is a step-by-step explanation:

1. SELECTEDVALUE Function

SELECTEDVALUE('XXX'[MeasureID], [Total Profit])

The SELECTEDVALUE function returns a single selected value from the 'XXX'[MeasureID] column if a value is selected in a filter or slicer.
If no value is selected, it returns the default value, which in this case is [Total Profit].

2. SWITCH Function

SWITCH (
    SELECTEDVALUE ( 'XXX'[MeasureID], [Total Profit] ),
    1, [Total Profit],
    2, [Total Sales],
    3, [Total Cost],
)
SWITCH works similarly to a CASE statement in other programming languages. It compares an expression (in this case, the result from SELECTEDVALUE) with the values provided in subsequent arguments.
When SELECTEDVALUE returns 1, 2, 3, 4, or 5, SWITCH returns the corresponding measure, i.e., [Total Profit], [Total Sales], [Total Cost].
----------------------------------

Step-by-Step Interpretation:
Step 1: The SELECTEDVALUE function checks if a value has been selected in the slicer or filter from the 'XXX'[MeasureID] column.
Step 2: If a specific value, e.g., 2, is selected, the result of SELECTEDVALUE is 2.
Step 3: The SWITCH function compares the result of SELECTEDVALUE with the values provided in its definition. If the result is 2, SWITCH returns [Total Sales].
Step 4: The result of this measure is one of the three measures, depending on the value selected in the slicer/filter.
-----------------------------------
![image](https://github.com/user-attachments/assets/294e2adf-e72c-4e4b-8643-f94d524d2b2e)

In order for the measure to work with the visualization, you need to change the “total sales” from the Y-axis to the new measure created.

![image](https://github.com/user-attachments/assets/73d6940e-6f05-479a-a612-5747c521c02e)


Everything works! ✨ This is the end of this guide !

I hope you will use it in your work 🚀

Best Regards, Mateusz Rajca


