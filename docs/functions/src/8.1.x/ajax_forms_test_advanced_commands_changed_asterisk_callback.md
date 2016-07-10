function **ajax_forms_test_advanced_commands_changed_asterisk_callback($form, FormStateInterface $form_state)**

> Ajax form callback: Selects 'changed' with asterisk marking inner div.

**Code:**
```php
function ajax_forms_test_advanced_commands_changed_asterisk_callback($form, FormStateInterface $form_state) {
  $response = new AjaxResponse();
  $response->addCommand(new ChangedCommand('#changed_div', '#changed_div_mark_this'));
  return $response;
}
```
