### Add custom submits or validators via hook_form_alter or hook_form_FORM_ID_alter:
```php
/**
 * Implements hook_form_alter().
 */
function my_module_form_alter(&$form, FormStateInterface $form_state, $form_id) {
  if ($form_id == 'test_form_drupalway') {
    // Add new submit and validator "functions". 
    $form['#submit'][] = 'my_module_test_submit';
    $form['#validate'][] = 'my_module_test_validate';
    // Add new submit and validation "method" inside the form builder.
    $form['#submit'][] = '::newFormSubmit';
    $form['#validate'][] = '::newFormValidate';
    // Add new submit and validation "method" from another class.
    $form['#submit'][] = '\Drupal\another_module\Forms\AnotherClass::newFormSubmit';
    $form['#validate'][] = '\Drupal\another_module\Forms\AnotherClass::newFormValidate';
  }
}
```