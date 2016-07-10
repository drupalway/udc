function **ajax_forms_test_lazy_load_form_ajax($form, FormStateInterface $form_state)**

> AJAX form callback: Selects for the ajax_forms_test_lazy_load_form() form.

**Code:**
```php
function ajax_forms_test_lazy_load_form_ajax($form, FormStateInterface $form_state) {
  $build = [
    '#markup' => 'new content',
  ];

  if ($form_state->getValue('add_files')) {
    $build['#attached']['library'][] = 'system/admin';
    $build['#attached']['library'][] = 'system/drupal.system';
    $build['#attached']['drupalSettings']['ajax_forms_test_lazy_load_form_submit'] = 'executed';
  }

  return $build;
}
```
