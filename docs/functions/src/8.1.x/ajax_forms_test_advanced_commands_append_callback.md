function **ajax_forms_test_advanced_commands_append_callback($form, FormStateInterface $form_state)**

> Ajax form callback: Selects 'append'.

**Code:**
```php
function ajax_forms_test_advanced_commands_append_callback($form, FormStateInterface $form_state) {
  $selector = '#append_div';
  $response = new AjaxResponse();
  $response->addCommand(new AppendCommand($selector, "Appended text"));
  return $response;
}
```
