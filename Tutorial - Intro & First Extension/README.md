![](files/arvato_hightech_emea_herobanner.jpg)

#  Tutorial objectives
* Understand the Magento Company and Products
* Have a rough understanding of most important Magento concepts 
* know how files are organized
* know the basic tasks for extending Magento
 
#  Who is Magento - A Company-Overview ##
 * 100%-owned by ebay since 2010
 * Subbrand listed under x.commerce
 * Headquarter in Los Angeles (USA)
 * Local subsidiaries in Berlin, London, Brussels and Dublin
 * Employee-count: ca. 400
 * > 150.000 installations world-wide
 
### Relating Magento to ebay:
![](files/ebay_company_diagram.jpg)

## How are they doing development?

 * 2 Edition available - Community Edition (CE) and Enterprise Edition (EE)
 * Both Editions are developed by the Magento Company itself, whereas the CE is always a few versions behind the EE
 * Apart from the version difference, EE contains more default extensions than CE

### Enterprise Only Features

* SolR Search (but extensions for CE available)
* Customer Segmentation with Targeted Offerings
* Dynamic - Rules-bades product relationships
* Automatic E-Mail Reminders
* Private Sales for custer groups (incl. Invitation)
* Gift Registry
* Gift Wrap Option
* Rebate Points Modul
* Several Wishlists per Customer
* Enhanced Catalog and Content Management System (CMS+)
* Staging, Merging and Rollback of Content
* Scheduled Publishing of Pages
* Customer-specific Profile Attributes
* Improved Performance (but you can achieve this with Varinish for CE)
* Payment Bridge
* Data Encrpytion and Key Management
* Call Center with Assisted Shopping
* Minimum Advertised Price
* Full-page Caching
* Customer Segmentation with Targeted Offerings
* Recurring Payments
* Full Page Caching

### Magento Connect  
Url: [http://www.magentocommerce.com/magento-connect/](http://www.magentocommerce.com/magento-connect/ "http://www.magentocommerce.com/magento-connect/")

## General Magento Concepts

* Magento is based on OOP and the Zend-Framework
* Module-based Architecture
* Event-Driven Architecture
* Configuration-Based

### MVC
 * Configuration-based Routing
 * Configuration-based Views (Layout+Blocks)
 * Thin-Controllers
 * Models contain Business Logic   
   
   ![](files/mvc.png)

### The Filesystem

**Top-Level**<br />
/ app - This is where the big stuff happens :)<br />
/ skin / {area} / {package} / {theme} / - is where design package css and images are<br />
/ lib - are libraries such as Zend and Varien<br />
/ js - where you put your javascripts<br />
/ media - uploaded files (product images, pdf documents, etc)<br />
/ tests - Unit tests (not done yet)<br />
/ var - temporary files<br />
/ includes - contains config.php<br />

**Inside the app folder**<br />
/ app / etc - global configuration. register your module with the system here<br />
/ app / code - is where modules have installed their models and controllers<br />
/ app / design - is location of design packages (layouts, templates, translations)<br />
/ app / locale - locale files<br />
<br />
**App code pools**<br />
/ app / code / core - are core team developed or certified modules<br />
/ app / code / community - are community contributed modules<br />
/ app / code / local - are local customizations<br />
<br />
**App design-reated**<br />
/ app / design / frontend - frontend design<br />
/ app / design / adminhtml - HTML admin panel design<br />
/ app / design / {area} / {package} / {theme} - theme customizations<br />
/ app / design / {area} / {package} / {theme} / layout - .xml files that define block structure for different cases in website flow<br />
/ app / design / {area} / {package} / {theme} / template - .phtml (html with php tags) templates<br />
/ app / design / {area} / {package} / {theme} / locale - Zend_Translate compatible translation files for package/theme<br />

/ app / locale / {locale (en\_US)} - Zend_Translate compatible translation files for modules<br />

**The Module structure**<br />
/ {Your  Code pool} / {Module} - module root<br />
/ {Your  Code pool} / {Module} / etc - module configuration<br />
/ {Your  Code pool} / {Module} / controllers - controllers provided by module<br />
/ {Your  Code pool} / {Module} / Block - Block logic classes<br />
/ {Your  Code pool} / {Module} / Model - Object Models provided by module<br />
/ {Your  Code pool} / {Module} / Model / Mysql4 - Resource Models provided by module<br />
/ {Your  Code pool} / {Module} / sql - sql installation and upgrade files between module versions<br />
/ {Your  Code pool} / {Module} / sql / {resource} / - resource model specific upgrades<br />


### Layout System

Layout and Design are separated from each other.<br />

####Important terms
**Design package**: is a collection of related themes. Each design package must have at least one default theme, but can contain any number of theme variants. (Christmas, holidays, etc.) /App/Design/Frontend/…

**Base package**: A special package that contains all the default elements for a Magento installation. 

**Default package**: This contains the layout elements of the default store (look and feel).

**Theme**: Part of a design package. Contains Layout Files, Template Files and Locale (optional). A theme can belong to only one design package. Every theme automatically included 4 basic layouts (one column, two columns with left sidebar, two column with right sidebar, three columns)

**Skin**: CSS, images, java script. Skins reside in a separate root folder named “Skin”. (Similar sub-tree like apps/design)

![](files/sample_skins.png)

**Layout-Files**: Define the hierarchical structure of a page. (footer, header, content, …) – XML Files. The structure is defined by handles, blocks and actions.
 Layout file always has a <layout> root node. The first child-level of this nodes are the “handles” (also called layout objects.). 

**Handles** are instantiated by the application controller’s action methods, and so the application logic decides which blocks get displayed. For doing that the controller code calls $this->loadLayout & $this->renderLayout. Handles contain blocks, which are the most important structural elements.

 ![](files/sample_layout_xml.png)

**Blocks:** Blocks can be seen as view models. Most blocks have a corresponding template file. Blocks contain PHP logic, templates contain HTML and PHP output code. Blocks refer directly back to the models for their data. In other words, the Action Controller does not pass them a data structure.
Blocks are hierarchical. Each block can contain any number of child blocks.


**Template-Files**: PHTML Files. – They define where the defined areas of the layout file appear in the rendered HTML page. To all of those files together, the documentation refers to as “template”. <br />*Note:* Whenever we use the `$this` keyword, we reference the instance of the related block object.

   ![](files/block-and-childblocks.png)


### Models
Magento models do not only contain data, but also the business logic (rich models), so usually the models are the most complex parts of a Magento solution.

#### Object Relational Mapping (ORM)

Magento models support Object Relational Mapping (ORM). Both the built in models and your own models use the Magento data access capabilities, so that no plain SQL has to be written by developers.

Magento supports two kinds of models:

* ActiveRecord-like/one-object-one-table models
* Entity Attribute Value (EAV) models

Each Magento model has also a model collection, which are similar to .NET collections (e.g. they can be used in for/as (= foreach in C#) loops.

Magento models do *not* contain any code for accessing the database directly, but they use a `modelResource` class to communicate with the database. Internally, one read and one write adapter is used.

#### Creating a Model

These are typical steps for creating a model that can be persisted in the database (we will perform these steps later on in the exercise part of this developer meeting):

1. Create a new model class
2. Create a database table for the model
3. Add model information to the configuration file of the module
4. Add model resource information to the configuration file of the module
5. Add a Read Adapter to the configuration file of the module
6. Add a Write Adapter to the configuration file of the module
7. Add a PHP class/file for the model
8. Add a PHP class/file for the resource model
9. Instantiate the model via Mage::getModel('<module_name>/<model_name>')

#### Setting and Getting Data on Models

Magento models inherit from `Varien_Object`. This class implements some functionality to access model data (via magic getters/setters). Internally, the whole functionality is built on a protected `_data` property which is an associative array. The `getData()` method can be used to get the whole associative array or only certain keys:

    $model->getData();
    $model->getData('some_property');

All database column names should contain only lowercase characters and should use underscores to separate the different words. Properties named in this way can be accessed directly via `get`, `set`, `unset`, `has`, and `is` like this (note that the `Varien_Object` camel-cases the property name):

    $model->getSomeProperty();
    $model->setSomeProperty('toSomeValue');
    $model->unsetSomeProperty();
    $hasSomeProperty = $model->hasSomeProperty();

In the exercise later on we will see how to retrieve data records from the database or how to save them.

#### The Entity Attribute Value Pattern (EAV)

For some entities (like products), Magento does not use simple (flat) database tables to store the information, but a more complicated, but highly flexible approach called Entity Attribute Value architecture (EAV). This makes the database structure a lot more complicated, but it allows to add an unlimited number of attributes to entities without having to change the database schema.

The EAV model allows vertical data modeling instead of the mostly used horizontal data modeling, which means that if a entity shall be extended by a new property, this is done by adding data records to certain tables, and not by adding a column to an existing table. That means that the Magento entities that are based on the EAV pattern can be extended by new properties without changing the database schema.

Important terms:

* **Entity**: e.g. products, categories, customers, customer addresses, etc.
* **Attribute**: the names of the items which belong to an entity, e.g. the title or the description of a product. It is important to understand that the attribute tables do not store the actual values, but only the metadata of the attribute.
* **Value**: Stores the values of the various attributes of the entities.

The following diagram shows the relationship between different database tables for products as an example:

![](files/eav.png)

Both the `catalog_product_entity` and the `eav_attribute` tables contain an `entity_type_id` column that is used to join the attributes to the product. The `eav_attribute` table contains a column `backend_type` that stores the datatype of the respective attribute. The actual values are stored in datatype specific tables like `catalog_product_entity_datetime`.

The EAV system is extendable by new entities, i.e. developers can create new EAV based entities.

**Pros and Cons**: EAV allows developers to extend the Magento system without the need to change existing data structures, so it adds a great deal of flexibility to the system. The downside is complexity and performance. The Magento base installation consists of more than 375 tables. In order to grab all the information for a single entity (like a product), a lot of different tables have to be joined together making the database the bottleneck of a Magento solution.

In order to bypass the performance bottleneck, the Magento developers decided to "cache" the information from the EAV tables into so-called index or flat tables. For categories and products, this feature can be turned on in the Magento backend (**System | Configuration | Catalog |** Expand **Frontend | Use Flat Catalog Category** and **Use Flat Catalog Product**).


## Developing a web log extension

Enough theory, it's time for a first Module. This walktrough tutorial is mainly derived from [Alan Storms Magento Developer Tutorial Part 3 and 5
](http://www.magentocommerce.com/knowledge-base/entry/magento-for-dev-part-3-magento-controller-dispatch) <br />

We're going to:

* Create a new "Weblog" module
* Create a database table for our Model
* Register a new Model
* Connect the model with the db - Register a ressource rodel
* Add a Read Adapter to the config for the Blogpost Model
* Add a Write Adapter to the config for the Blogpost Model
* Add a PHP class file for the Blogpost Model
* Add a PHP class file for the Blogpost Resource Model
* Instantiate the Model

### Create a new module called "Weblog"

First, we'll create a directory structure for this module. Our directory structure should look as follows:

app/code/local/Magentotutorial/Weblog/Block<br />
app/code/local/Magentotutorial/Weblog/controllers<br />
app/code/local/Magentotutorial/Weblog/etc<br />
app/code/local/Magentotutorial/Weblog/Helper<br />
app/code/local/Magentotutorial/Weblog/Model<br />
app/code/local/Magentotutorial/Weblog/sql<br />

Then create a configuration file for the module (at path app/code/local/Magentotutorial/Weblog/etc/config.xml):

<!-- language: lang-xml -->

	<config>
	    <modules>
	        <Magentotutorial_Weblog>
	            <version>0.1.0</version>
	        </Magentotutorial_Weblog>
	    </modules>
	</config>

Then create a file to activate the module (at path app/etc/modules/Magentotutorial_Weblog.xml):

<!-- language: lang-xml -->
	
	<config>
	    <modules>
	        <Magentotutorial_Weblog>
	            <active>true</active>
	            <codePool>local</codePool>
	        </Magentotutorial_Weblog>
	    </modules>
	</config>

Finally, we ensure the module is active. - Clear your Magento cache.

* In the Magento Admin, go to System->Configuration->Advanced.
* Expand "Disable Modules Output" (if it isn't already).
* Ensure that Magentotutorial_Weblog shows up.

### Create Action Controller(s) for our Routes

Create a file at app/code/local/Magentotutorial/Weblog/controllers/IndexController.php

That contains the following

<!-- language: lang-php -->

	class Magentotutorial_Weblog_IndexController extends Mage_Core_Controller_Front_Action {        
	
	    public function testModelAction() {
           echo 'Setup!';
        }
	
	}
	
### Configuring Routes
Next, we're going to configure a route. A route will turn a URL into an Action Controller and a method. Unlike other convention based PHP MVC systems, with Magento you need to explicitly define a route in the global Magento config.

In your config.xml file, add the following section:

<!-- language: lang-xml -->

	<config>    
	    ...
	    <frontend>
	       <routers>
	        <weblog>
	            <use>standard</use>
	            <args>
	                <module>Magentotutorial_Weblog</module>
	                <frontName>weblog</frontName>
	            </args>
	        </weblog>
	    </routers>
	    </frontend>
	    ...
	</config>

#### Understand the routing

The `<frontend>` tag refers to a Magento Area. There are mainly two of them <admin> and <frontend>.<br />
The `<routers>` tag contains all custom registered routes.<br />

When a router parses a URL, it gets separated as follows

	http://example.com/frontName/actionControllerName/actionMethod/

So, by defining a value of "weblog" in the `<frontName>` tags, we're telling Magento that we want the system to respond to URLs in the form of

	http://example.com/weblog/*

This module tag should be the full name of your module, including its package/namespace name. This will be used by the system to locate your Controller files.

#### Testing the registered action

Clear your config cache, and load the following URL

	http://exmaple.com/weblog/index/testModel
	
You should see the word "Setup" on a white background. Congratulations, you've setup your first Magento Controller!

### Create a database table for our Model

Magento has a system for automatically creating and changing your database schemas, but for the time being we'll just manually create a table for our Model.

Using the command-line or your favorite MySQL GUI application, create a table with the following schema

<!-- language: lang-sql -->

	CREATE TABLE `blog_posts` (
	  `blogpost_id` int(11) NOT NULL auto_increment,
	  `title` text,
	  `post` text,
	  `date` datetime default NULL,
	  `timestamp` timestamp NOT NULL default CURRENT_TIMESTAMP,
	  PRIMARY KEY  (`blogpost_id`)
	)

And then populate it with some data
	
	INSERT INTO `blog_posts` VALUES (1,'My New Title','This is a blog post','2010-07-01 00:00:00','2010-07-02 23:12:30');



### Register a new Model

When you instantiate a Model in Magento, you make a call like this

<!-- language: lang-php -->

	$model = Mage::getModel('weblog/blogpost');

the first part of the URI you pass into get Model is the Model Group Name. Because it is a good idea to follow conventions, this should be the (lowercase) name of your module, or to be safeguarded agains conflicts use the packagename and modulename (also in lowercase). The second part of the URI is the lowercase version of your Model name.

So, let's add the following XML to our module's config.xml.
	
<!-- language: lang-xml -->

	<global>
	    <!-- ... -->
	    <models>
	        <weblog>
	            <class>Magentotutorial_Weblog_Model</class>
	            <!--
	            need to create our own resource, cant just
	            use core_resource
	            -->
	            <resourceModel>weblog_resource</resourceModel>
	        </weblog>
	    </models>
	    <!-- ... -->
	</global>

`<weblog />` is your Group Name, which should match your module name.<br />
`<class />` is the BASE name all Models in the weblog group will have.<br />
`<resourceModel />` indicates which Resource Model that weblog group Models should use.

So, we're not done yet, but let's see what happens if we clear our Magento cache and attempt to instantiate a blogpost Model. In your testModelAction method, use the following code

<!-- language: lang-php -->

	public function testModelAction() {
	        $blogpost = Mage::getModel('weblog/blogpost');
	        echo get_class($blogpost);
	    }
	
and reload your page. You should see an exception that looks something like this (be sure you've turned on developer mode).

	include(Magentotutorial/Weblog/Model/Blogpost.php) [function.include]: failed to open stream: No such file or directory

Magento is trying to __autoload include this Model, but can't find the file. Let's create it! Create the following class at the following location

	File: app/code/local/Magentotutorial/Weblog/Model/Blogpost.php

<!-- language: lang-php -->

	class Magentotutorial_Weblog_Model_Blogpost extends Mage_Core_Model_Abstract
	{
	    protected function _construct()
	    {
	        $this->_init('weblog/blogpost');
	    }
	}

		
### Connect the model with the db - Register a ressource rodel

So, we've setup our Model. Next, we need to setup our Model Resource. Model Resources contain the code that actually talks to our database. In the last section, we included the following in our config.

	<resourceModel>weblog_resource</resourceModel>

The value in `<resourceModel />` will be used to instantiate a Model Resource class. Although you'll never need to call it yourself, when any Model in the weblog group needs to talk to the database, Magento will make the following method call to get the Model resource

	Mage::getResourceModel('weblog/blogpost');

Again, weblog is the Group Name, and blogpost is the Model. The Mage::getResourceModel method will use the weblog/blogpost URI to inspect the global config and pull out the value in `<resourceModel>` (in this case, weblog_resource). Then, a model class will be instantiated with the following URI

	weblog_resource/blogpost

So, if you followed that all the way, what this means is, resource models are configured in the same section of the XML config as normal Models. This can be confusing to newcomers and old-hands alike.

So, with that in mind, let's configure our resource. In our <models> section add

<!-- language: lang-xml -->

	<global>
	    <!-- ... -->
	    <models>
	        <!-- ... -->
	        <weblog_resource>
	            <class>Magentotutorial_Weblog_Model_Resource</class>
	        </weblog_resource>
	    </models>
	</global>

You're adding the `<weblog_resource />` tag, which is the value of the `<resourceModel />` tag you just setup. The value of` <class />` is the base name that all your resource modes will have, and should be named with the following format

	Packagename_Modulename_Model_Resource

So, we have a configured resource, let's try loading up some Model data. Change your action to look like the following

<!-- language: lang-php -->

	public function testModelAction() {
	    $params = $this->getRequest()->getParams();
	    $blogpost = Mage::getModel('weblog/blogpost');
	    echo("Loading the blogpost with an ID of ".$params['id']);
	    $blogpost->load($params['id']);
	    $data = $blogpost->getData();
	    var_dump($data);
	}

Add the following class at at the following location

	File: app/code/local/Magentotutorial/Weblog/Model/Resource/Blogpost.php

<!-- language: lang-php -->

	class Magentotutorial_Weblog_Model_Resource_Blogpost extends Mage_Core_Model_Resource_Db_Abstract{
	    protected function _construct()
	    {
	        $this->_init('weblog/blogpost', 'blogpost_id');
	    }
	}

Now load the following URL in your browser (after clearing your Magento cache)

	http://example.com/weblog/index/testModel/id/1

You should see

	Can't retrieve entity config: weblog/blogpost

When we use the Model URI weblog/blogpost, we're telling Magento we want the Model Group weblog, and the blogpost Entity. In the context of simple Models that extend Mage_Core_Model_Resource_Db_Abstract, an entity corresponds to a table. In this case, the table named blog_post that we created above. 

Let's add that entity to our XML config.

<!-- language: lang-php -->

	<models>
	   <!-- ... --->
	   <weblog_resource>
	     <class>Magentotutorial_Weblog_Model_Resource</class>
	     <entities>
	        <blogpost>
	           <table>blog_posts</table>
	        </blogpost>
	     </entities>
	  </weblog_resource>
	</models>

Clear your Magento cache, cross your fingers, reload the page and ...

	Loading the blogpost with an ID of 1
	
	array
	  'blogpost_id' => string '1' (length=1)
	  'title' => string 'My New Title' (length=12)
	  'post' => string 'This is a blog post' (length=19)
	  'date' => string '2009-07-01 00:00:00' (length=19)
	  'timestamp' => string '2009-07-02 16:12:30' (length=19)

### Use the new model and data access in the controller

Add the following method to your Controller

<!-- language: lang-php -->

	public function createNewPostAction() {
	    $blogpost = Mage::getModel('weblog/blogpost');
	    $blogpost->setTitle('Code Post!');
	    $blogpost->setPost('This post was created from code!');
	    $blogpost->save();
	    echo 'post with ID ' . $blogpost->getId() . ' created';
	}
	
	public function editFirstPostAction() {
	    $blogpost = Mage::getModel('weblog/blogpost');
	    $blogpost->load(1);
	    $blogpost->setTitle("The First post!");
	    $blogpost->save();
	    echo 'post edited';
	}
	
	public function deleteFirstPostAction() {
	    $blogpost = Mage::getModel('weblog/blogpost');
	    $blogpost->load(1);
	    $blogpost->delete();
	    echo 'post removed';
	}

	public function showAllBlogPostsAction() {
	    $posts = Mage::getModel('weblog/blogpost')->getCollection();
	    foreach($posts as $blogpost){
	        echo '<h3>'.$blogpost->getTitle().'</h3>';
	        echo nl2br($blogpost->getPost());
	    }
	}
	
Now execute your Controller Action by loading the following URLs:

	http://example.com/weblog/index/createNewPost
	http://example.com/weblog/index/showAllBlogPosts
	
The first works, the second not. We need to add a PHP class file that defines our Blogpost collection. Every Model has a protected property named _resourceCollectionName that contains a URI that's used to identify our collection.

Magento considers Collections part of the Resource, so this URI is converted into the class name. So the ressource identifier is translated into a type name like this:

	'weblog/blogpost_collection' => Magentotutorial_Weblog_Model_Resource_Blogpost_Collection

So we have to add the following PHP class at the following location

	File: app/code/local/Magentotutorial/Weblog/Model/Resource/Blogpost/Collection.php

<!-- language: lang-php -->

	class Magentotutorial_Weblog_Model_Resource_Blogpost_Collection extends Mage_Core_Model_Resource_Db_Collection_Abstract {
	    protected function _construct()
	    {
	            $this->_init('weblog/blogpost');
	    }
	}
	

## Links

* [Magento for Developers: Part 3 - Magento Controller Dispatch](http://www.magentocommerce.com/knowledge-base/entry/magento-for-dev-part-3-magento-controller-dispatch)
* [Magento for Developers: Part 5 - Magento Models and ORM Basics](http://www.magentocommerce.com/knowledge-base/entry/magento-for-dev-part-5-magento-models-and-orm-basics)

## Material for self-studying Magento

Books:
 * 




