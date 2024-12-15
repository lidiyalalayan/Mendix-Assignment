# How to Create a Basic Hardware Store Inventory App
## 1 Introduction
This document provides step by step guidance on how to create an app for the purpose of hardware store inventory. Here, you will learn how to extend the existing Blank Web App by handling data, populating your app’s pages with widgets/blocks and creating custom app logic using a microflow.
## 2 Prerequisites
Before you start, make sure to Install **Mendix Studio Pro**. Please refer to the following articles for instructions on how to install the application.

* [Installing Mendix Studio pro on Windows](https://docs.mendix.com/refguide/install/)
* [Installing Mendix Studio Pro on Mac](https://docs.mendix.com/refguide/using-mendix-studio-pro-on-a-mac/)
## 3 Setting Up the Home Page 
You have now access to the environment and can start extending your **TW-2403** app. 

Start by navigating to your **Home_Web** page on the left-sided structural pane below **MyFirstModule**. This page offers basic navigation functionalities. Enrich your page by adding  a Card Action block  which you will later use to navigate to another page. Follow these steps:

1. Locate the **Card Action** block from the Toolbox located on the right-sided pane and drag it onto the page. 
2. Change the name of the block to ‘Tools’. 
## 4 Adding the Tools Entity
It is essential to create an persistable [entity](https://docs.mendix.com/refguide/entities/) in order to store your data and populate your app with inventory information in Mendix Studio Pro. Right-click the **Domain Model** below **MyFirstModule** and drag **Entity** onto your working area from the toolbox on the right pane. 

![image1]([https://github.com/lidiyalalayan/Mendix-Assignment/blob/102198c1e15d80a8945d4578590d5d9804117e11/Screenshot%202024-12-13%20164721.jpg](https://github.com/lidiyalalayan/Mendix-Assignment/blob/main/Screenshot%202024-12-15%20150139.jpg))

Double-click the entity and create two new attributes, **Name** and **Code**, by clicking **New** in the tab Attributes. These are small information pieces about your entity, which in this case will contain the name and the code of each tool. 

![image2]([https://github.com/lidiyalalayan/Mendix-Assignment/edit/main/TW-2403#:~:text=Screenshot%202024%2D12%2D-,14%20133908,-.jpg](https://github.com/lidiyalalayan/Mendix-Assignment/blob/main/Screenshot%202024-12-14%20133908.jpg))

Double-click the entity and name it ‘Tools’ from the **General** settings. You are now all set.

![image3](https://github.com/lidiyalalayan/Mendix-Assignment/blob/main/Screenshot%202024-12-13%20165049.jpg)
## 5 Setting Up the Tools Page
Right-click **MyFirstModule** on the left-sided pane and select **Add page**. Name this page ‘Tools’. 

Add two new **Card action** blocks to the **Tools** page. These blocks will allow navigation to the two main areas of the app where your users can view and edit the stock information. Double-click the text area of each block to edit the text that you would like to display. In the Caption box of the popup, write the following texts:

* Display and search tools
* Add and edit tools

You can also choose to add tooltip text on the buttons to improve the overall user interface.
## 6 Setting Up the Tools List Page
Now it is time to create a page where users can search the stock of tools and visualize it. To start, create a page as described in the previous section and name it ‘Tools_ListView’. Add a **List view** widget to the page from the Toolbox on the right pane. 

You will now be able to connect the **Tools** entity that you have created previously as a data source to your **List view** widget. Simply double-click the widget, go to the **Data Source** tab and select the **Tools** entity for **Entity(path)*.

![image4](https://github.com/lidiyalalayan/Mendix-Assignment/blob/main/Screenshot%202024-12-14%20144234.jpg)

In order to display the **Name** and **Code** attributes on top of each other and improve the user interface, use the **Text** widget. 

1. Place the text widget named ‘Tool name: ‘ before the **{Name}**.
2. Place the text widget named ‘Tool code: ‘ before the **{Code}**.
3. Double-click the **Tool code** text and add a line break in the caption as following:

![image5](https://github.com/lidiyalalayan/Mendix-Assignment/blob/main/Screenshot%202024-12-14%20152138.jpg)

Your page is now ready to store the data of the inventory tools.
## 7 Setting Up the Tools Edit Page
This page will enable app users to conduct several operations such as searching, editing, creating, and deleting tools from the inventory. 

Let's start by dragging a *Data grid** block onto the newly created **Tools_EditGrid** page. Double-click the block and choose **Tools** as the **Entity(path)**. You can notice two **error** messages on the pane below the Working area.

![image6](https://github.com/lidiyalalayan/Mendix-Assignment/blob/main/Screenshot%202024-12-15%20154049.jpg)

These errors indicate that the **New** and **Edit** buttons both require an on click page. Create a new **Tools_AddNew** page. Go to the General setting of the **New** button and select this page.

![image7](https://github.com/lidiyalalayan/Mendix-Assignment/blob/main/Screenshot%202024-12-13%20205225.jpg)

The **Edit** button of your block automatically inherits the same setting as the **New** button.
## 8 Setting Up the Add Tools Page
The page Tools_AddNew  that you have created previously is intended for adding and editing information on the new tools of your user’s  inventory. Drag the **Data view** widget onto the page and relate the **Tools** entity to the widget. 
### 8.1 Adding a Microflow to Save Button
Now, you need to apply logic to the **Save** button. You can achieve that by creating a [microflow](https://docs.mendix.com/refguide/microflows/), which executes a series of actions when the requirements are met. 

1. Double-click the **Save** button, and open the General settings.
2. Select **Call a microflow** as an on click event. 

![image8](https://github.com/lidiyalalayan/Mendix-Assignment/blob/main/Screenshot%202024-12-14%20142705.jpg)

3. A new pop-up page will appear. Select the **New** button.
4. Name the microflow ‘Tools_ValidateAndSaveNew’ and press **OK**.

You will now be able to see your Tools_ValidateAndSaveNew microflow on the left-sided structural pane. Open the microflow and start adding elements to it.

1. Drag the **Parameter** element onto the microflow to the working area. Double-click it, select the data type **Object** and choose the entity **Tools**.This will connect the parameter to the Tools entity in order to relate it to the microflow.

![image9](https://github.com/lidiyalalayan/Mendix-Assignment/blob/main/Screenshot%202024-12-15%20154742.jpg)

2. Drag the **Decision** element onto the microflow, double-click it and add the following line of code into the expression box: *$Tools/Name != empty and trim($Tools/Name) != '' and $Tools/Code != empty and trim($Tools/Code) != ''*. This expression checks that both the **Name** and the **Code** attributes contain data and are not just empty spaces.

![image10](https://github.com/lidiyalalayan/Mendix-Assignment/blob/main/Screenshot%202024-12-15%20154756.jpg)

3. On the true path, add the **Commit object(s)** element to the microflow. Commit to tools [object](https://docs.mendix.com/refguide/committing-objects/) as demonstrated below. 

![image11](https://github.com/lidiyalalayan/Mendix-Assignment/blob/main/Screenshot%202024-12-15%20154816.jpg)

4. Add the **Show message** element on the true path. Select **New** in the parameter box and add *$Tools/Name* as a parameter. Afterwards, insert the message of success: ‘The tool *"{1}"* was saved successfully!’ into the Template box.

![image12](https://github.com/lidiyalalayan/Mendix-Assignment/blob/main/Screenshot%202024-12-15%20154952.jpg)

5. On the true path, add the **Show** page element and select **Tools_EditGrid** page. This will redirect the user to the page where they can add another tool, providing a smooth transition back to the Tools_EditGrid page.
6. On the false path, insert the **Show message** element  for when the requirements are not met. Select the type of message as Error, and add the following message to the template box: ‘Error! Both "Name" and "Code" must contain data in order to save a tool. Please try again.’

Now that you are all set with the microflow creation you need to add [validation](https://docs.mendix.com/refguide/setting-up-data-validation/) rules on **Tools** entity level. To prevent your app users from creating duplicates of the same tool you need to have a **Unique** rule for each **Name** and **Code** attributes.

* Attention! A tool with this name already exists. Please choose a different name.
* Attention! A tool with this code already exists. Please choose a different code.

![image13](https://github.com/lidiyalalayan/Mendix-Assignment/blob/main/Screenshot%202024-12-15%20154952.jpg)

## 9 Improving the Navigation and Publishing the App
In order to improve the reverse navigation between pages, you can place **Button** widgets on each page. Make sure to provide the correct path to each button that will eventually lead to the desired flow. This can be achieved by following the same steps as previously described for the Action Card block’s  button. You can also set the caption, the tooltip and the icon to improve your widgets’ look.

![image14](https://github.com/lidiyalalayan/Mendix-Assignment/blob/main/Screenshot%202024-12-15%20154952.jpg)

Now it is time to test your app. Press the **Run locall**y button, wait a few seconds and then click the **Press View** app button to preview your app in the browser. When you are happy with your app, **Publish** it. All of this can be performed from the top bar of Mendix Studio Pro .

![image15](https://github.com/lidiyalalayan/Mendix-Assignment/blob/main/Screenshot%202024-12-15%20160204.jpg)

## Read more
* [Create Your First Two Overview and Detail Pages | Mendix Documentation](https://docs.mendix.com/howto/front-end/create-your-first-two-overview-and-detail-pages/)
* [Building Block | Mendix Documentation](https://docs.mendix.com/refguide/building-block/#:~:text=To%20create%20a%20building%20block,blocks%20tab%20of%20the%20Toolbox.)
* [Creating a Custom Save Button with a Microflow | Mendix Documentation](https://docs.mendix.com/refguide/creating-a-custom-save-button/)
* [String Function Calls | Mendix Documentation](https://docs.mendix.com/refguide/string-function-calls/)
