function **ajax_forms_test_advanced_commands_alert_callback($form, FormStateInterface $form_state)**

> Ajax form callback: Selects 'alert'.

**Code:**
```php
function ajax_forms_test_advanced_commands_alert_callback($form, FormStateInterface $form_state) {
  $response = new AjaxResponse();
  $response->addCommand(new AlertCommand('Alert'));
  return $response;
}
```
