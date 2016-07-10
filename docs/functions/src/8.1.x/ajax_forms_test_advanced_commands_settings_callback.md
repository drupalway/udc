function **ajax_forms_test_advanced_commands_settings_callback($form, FormStateInterface $form_state)**

> Ajax form callback: Selects 'settings'.

**Code:**
```php
function ajax_forms_test_advanced_commands_settings_callback($form, FormStateInterface $form_state) {
  $setting['ajax_forms_test']['foo'] = 42;
  $response = new AjaxResponse();
  $response->addCommand(new SettingsCommand($setting));
  return $response;
}
```
