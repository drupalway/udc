function **ajax_forms_test_advanced_commands_insert_callback($form, FormStateInterface $form_state)**

> Ajax form callback: Selects 'insert'.

**Code:**
```php
function ajax_forms_test_advanced_commands_insert_callback($form, FormStateInterface $form_state) {
  $response = new AjaxResponse();
  $response->addCommand(new InsertCommand('#insert_div', 'insert replacement text'));
  return $response;
}
```
