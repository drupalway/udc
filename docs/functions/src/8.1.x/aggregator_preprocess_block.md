function **aggregator_preprocess_block(&$variables)**

> Implements hook_preprocess_HOOK() for block templates.

**Code:**
```php
function aggregator_preprocess_block(&$variables) {
  if ($variables['configuration']['provider'] == 'aggregator') {
    $variables['attributes']['role'] = 'complementary';
  }
}
```
