function **ajax_forms_test_validation_form_callback($form, FormStateInterface $form_state)**

> Ajax form callback: Selects the 'drivertext' element of the validation form.

**Code:**
```php
function ajax_forms_test_validation_form_callback($form, FormStateInterface $form_state) {
  drupal_set_message("ajax_forms_test_validation_form_callback invoked");
  drupal_set_message(t("Callback: drivertext=%drivertext, spare_required_field=%spare_required_field", array('%drivertext' => $form_state->getValue('drivertext'), '%spare_required_field' => $form_state->getValue('spare_required_field'))));
  return ['#markup' => '<div id="message_area">ajax_forms_test_validation_form_callback at ' . date('c') . '</div>'];
}
```
