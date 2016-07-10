function **action_entity_type_build(array &$entity_types)**

> Implements hook_entity_type_build().

**Code:**
```php
function action_entity_type_build(array &$entity_types) {
  /** @var $entity_types \Drupal\Core\Entity\EntityTypeInterface[] */
  $entity_types['action']
  ->setFormClass('add', 'Drupal\action\ActionAddForm')
    ->setFormClass('edit', 'Drupal\action\ActionEditForm')
    ->setFormClass('delete', 'Drupal\action\Form\ActionDeleteForm')
    ->setListBuilderClass('Drupal\action\ActionListBuilder')
    ->setLinkTemplate('delete-form', '/admin/config/system/actions/configure/{action}/delete')
    ->setLinkTemplate('edit-form', '/admin/config/system/actions/configure/{action}')
    ->setLinkTemplate('collection', '/admin/config/system/actions');
}
```
