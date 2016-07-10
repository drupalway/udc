function **ajax_forms_test_advanced_commands_add_css_callback($form, FormStateInterface $form_state)**

> Ajax callback for 'add_css'.

**Code:**
```php
function ajax_forms_test_advanced_commands_add_css_callback($form, FormStateInterface $form_state) {
  $response = new AjaxResponse();
  $response->addCommand(new AddCssCommand('my/file.css'));
  return $response;
}
```
