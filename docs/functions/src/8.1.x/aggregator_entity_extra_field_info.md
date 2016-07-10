function **aggregator_entity_extra_field_info()**

> Implements hook_entity_extra_field_info().

**Code:**
```php
function aggregator_entity_extra_field_info() {
  $extra = array();

  $extra['aggregator_feed']['aggregator_feed'] = array(
    'display' => array(
      'items' => array(
        'label' => t('Items'),
        'description' => t('Items associated with this feed'),
        'weight' => 0,
      ),
      // @todo Move to a formatter at https://www.drupal.org/node/2339917.
      'image' => array(
        'label' => t('Image'),
        'description' => t('The feed image'),
        'weight' => 2,
      ),
      // @todo Move to a formatter at https://www.drupal.org/node/2149845.
      'description' => array(
        'label' => t('Description'),
        'description' => t('The description of this feed'),
        'weight' => 3,
      ),
      'more_link' => array(
        'label' => t('More link'),
        'description' => t('A more link to the feed detail page'),
        'weight' => 5,
      ),
      'feed_icon' => array(
        'label' => t('Feed icon'),
        'description' => t('An icon that links to the feed URL'),
        'weight' => 6,
      ),
    ),
  );

  $extra['aggregator_item']['aggregator_item'] = array(
    'display' => array(
      // @todo Move to a formatter at https://www.drupal.org/node/2149845.
      'description' => array(
        'label' => t('Description'),
        'description' => t('The description of this feed item'),
        'weight' => 2,
      ),
    ),
  );

  return $extra;
}
```
