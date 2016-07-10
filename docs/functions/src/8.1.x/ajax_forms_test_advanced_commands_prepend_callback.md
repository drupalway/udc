function **ajax_forms_test_advanced_commands_prepend_callback($form, FormStateInterface $form_state)**

> Ajax form callback: Selects 'prepend'.

**Code:**
```php
function ajax_forms_test_advanced_commands_prepend_callback($form, FormStateInterface $form_state) {
  $response = new AjaxResponse();
  $response->addCommand(new PrependCommand('#prepend_div', "prepended text"));
  return $response;
}
```
