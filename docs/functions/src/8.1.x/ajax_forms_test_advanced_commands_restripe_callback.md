function **ajax_forms_test_advanced_commands_restripe_callback($form, FormStateInterface $form_state)**

> Ajax form callback: Selects 'restripe'.

**Code:**
```php
function ajax_forms_test_advanced_commands_restripe_callback($form, FormStateInterface $form_state) {
  $response = new AjaxResponse();
  $response->addCommand(new RestripeCommand('#restripe_table'));
  return $response;
}
```
