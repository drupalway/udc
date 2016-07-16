## Adding route for the custom form in *.routing.yml file:
### Create a route name.
Route name should be prefixed with a module name and trailing dot.
```yml
my_module.test_form:
...
```
### Add path.
A relative path for you custom page, where the form should be placed.
```yml
my_module.test_form:
  path: 'testform/drupalway'
```
### Specify the form builder class.
A full namespace to the class which implements the form builder functionality.
```yml
my_module.test_form:
  path: 'testform/drupalway'
  defaults:
    _form: '\Drupal\my_module\Forms\TestFormDrupalway'
```
### Add form title.
[optional] Page title.
```yml
my_module.test_form:
  path: 'testform/drupalway'
  defaults:
    _form: '\Drupal\my_module\Forms\TestFormDrupalway'
    _title: 'Test form'
```
### Set permissions.
[optional] Permissions to restrict the access for this form.
```yml
my_module.test_form:
  path: 'testform/drupalway'
  defaults:
    _form: '\Drupal\my_module\Forms\TestFormDrupalway'
    _title: 'Test form'
  requirements:
    _permission: 'access content'
```


### Full example:
```yml
my_module.test_form:
  path: 'testform/drupalway'
  defaults:
    _form: '\Drupal\my_module\Forms\TestFormDrupalway'
    _title: 'Test form'
  requirements:
    _permission: 'access content'

```