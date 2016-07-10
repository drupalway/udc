function **ajax_forms_test_validation_number_form_callback($form, FormStateInterface $form_state)**

> Ajax form callback: Selects the 'drivernumber' element of the validation form.

**Code:**
```php
function ajax_forms_test_validation_number_form_callback($form, FormStateInterface $form_state) {
  drupal_set_message("ajax_forms_test_validation_number_form_callback invoked");
  drupal_set_message(t("Callback: drivernumber=%drivernumber, spare_required_field=%spare_required_field", array('%drivernumber' => $form_state->getValue('drivernumber'), '%spare_required_field' => $form_state->getValue('spare_required_field'))));
  return ['#markup' => '<div id="message_area_number">ajax_forms_test_validation_number_form_callback at ' . date('c') . '</div>'];
}
```
