function **ajax_forms_test_advanced_commands_data_callback($form, FormStateInterface $form_state)**

> Ajax form callback: Selects 'data'.

**Code:**
```php
function ajax_forms_test_advanced_commands_data_callback($form, FormStateInterface $form_state) {
  $selector = '#data_div';
  $response = new AjaxResponse();
  $response->addCommand(new DataCommand($selector, 'testkey', 'testvalue'));
  return $response;
}
```
