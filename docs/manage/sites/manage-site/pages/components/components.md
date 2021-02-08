# [Components](./components.md)

By default the CMS has only the following components:

+ List Posts
+ View Post
+ Static Post
+ List Categories
+ List Category Posts

Other components can be added via [extra modules](./../../../../../extending/extending.md).



### **List Posts**
Will place all posts of the site on the "posts" variable, it supports pagination via "pagination" to show only a subset of posts at a time.

### **View Posts**
This component receives a post slug as a parameter. The post is place on the "post" variable to be displayed.

### **Static Posts**
This component is associated with a single post. The post is place on the "post" variable to be displayed.

### **List Categories**
Lists all categories present on the site. The list is accessible via  the "categories" variable.

### **List Category Posts**
Displays a list with all posts of a category set for this component. Otherwise it behaves just like the List Posts component, exposing both "pages" and "pagination".

 