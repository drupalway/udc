function **ajax_forms_test_advanced_commands_before_callback($form, FormStateInterface $form_state)**

> Ajax form callback: Selects 'before'.

**Code:**
```php
function ajax_forms_test_advanced_commands_before_callback($form, FormStateInterface $form_state) {
  $selector = '#before_div';
  $response = new AjaxResponse();
  $response->addCommand(new BeforeCommand($selector, "Before text"));
  return $response;
}
```
