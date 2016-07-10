function **ajax_forms_test_advanced_commands_invoke_callback($form, FormStateInterface $form_state)**

> Ajax form callback: Selects 'invoke'.

**Code:**
```php
function ajax_forms_test_advanced_commands_invoke_callback($form, FormStateInterface $form_state) {
  $response = new AjaxResponse();
  $response->addCommand(new InvokeCommand('#invoke_div', 'addClass', array('error')));
  return $response;
}
```
