function **action_views_form_substitutions()**

> Implements hook_views_form_substitutions().

**Code:**
```php
function action_views_form_substitutions() {
  $select_all = array(
    '#type' => 'checkbox',
    '#default_value' => FALSE,
    '#attributes' => array('class' => array('action-table-select-all')),
  );
  return array(
    '<!--action-bulk-form-select-all-->' => drupal_render($select_all),
  );
}
```
