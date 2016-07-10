function **ajax_forms_test_advanced_commands_after_callback($form, FormStateInterface $form_state)**

> Ajax form callback: Selects 'after'.

**Code:**
```php
function ajax_forms_test_advanced_commands_after_callback($form, FormStateInterface $form_state) {
  $selector = '#after_div';

  $response = new AjaxResponse();
  $response->addCommand(new AfterCommand($selector, "This will be placed after"));
  return $response;
}
```
