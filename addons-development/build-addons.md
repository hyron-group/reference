# build-addons

\[ experiment \]

Addons is a very simple and powerful feature. It allows you to customize and extend Hyron framework. By allowing access to resources that are managed from the ModuleManager class ( base of Hyron ) via this scope

## Declaration syntax

The simple addons are a function that is loaded into this variable from an initialized instance

```javascript
function myAddons(){
    // show baseURI
    console.log(this.baseURI)
}
```

through this variable, you can optionally load what you want by using the following ways :

```javascript
// way 1 : used object.assign for multi value
Object.assign(this, args) // merge this var with args

// way 2 : used load var for single value
this.var_name = val'
```

You can also use the above method to override the default method. However, that is not recommended. If it's a bundle of Hyrons, we'd love to be able to contribute an edit from you.

To develop addons effectively, in addition to the documentation we have developed, you can study Hyron code to get a better view of the framework.
