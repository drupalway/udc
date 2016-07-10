function **aggregator_theme()**

> Implements hook_theme().

**Code:**
```php
function aggregator_theme() {
  return array(
    'aggregator_feed' => array(
      'render element' => 'elements',
      'file' => 'aggregator.theme.inc',
    ),
    'aggregator_item' => array(
      'render element' => 'elements',
      'file' => 'aggregator.theme.inc',
    ),
  );
}
```
