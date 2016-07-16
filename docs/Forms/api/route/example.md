### Add route for the custom form in *.routing.yml file:
```yml
my_module.test_form:
  path: 'testform/drupalway'
  defaults:
    _form: '\Drupal\my_module\Forms\TestFormDrupalway'
    _title: 'Test form'
  requirements:
    _permission: 'access content'

```