function **ajax_forms_test_advanced_commands_changed_callback($form, FormStateInterface $form_state)**

> Ajax form callback: Selects 'changed'.
  
**Code:**
```php
function ajax_forms_test_advanced_commands_changed_callback($form, FormStateInterface $form_state) {
  $response = new AjaxResponse();
  $response->addCommand(new ChangedCommand('#changed_div'));
  return $response;
}
```
