function **ajax_forms_test_advanced_commands_remove_callback($form, FormStateInterface $form_state)**

> Ajax form callback: Selects 'remove'.

**Code:**
```php
function ajax_forms_test_advanced_commands_remove_callback($form, FormStateInterface $form_state) {
  $response = new AjaxResponse();
  $response->addCommand(new RemoveCommand('#remove_text'));
  return $response;
}
```
