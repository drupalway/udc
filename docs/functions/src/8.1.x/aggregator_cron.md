function **aggregator_cron()**

> Implements hook_cron().

> Queues news feeds for updates once their refresh interval has elapsed.

**Code:**
```php
function aggregator_cron() {
  $queue = \Drupal::queue('aggregator_feeds');

  $ids = \Drupal::entityManager()->getStorage('aggregator_feed')->getFeedIdsToRefresh();
  foreach (Feed::loadMultiple($ids) as $feed) {
    if ($queue->createItem($feed)) {
      // Add timestamp to avoid queueing item more than once.
      $feed->setQueuedTime(REQUEST_TIME);
      $feed->save();
    }
  }

  // Delete queued timestamp after 6 hours assuming the update has failed.
  $ids = \Drupal::entityQuery('aggregator_feed')
    ->condition('queued', REQUEST_TIME - (3600 * 6), '<')
    ->execute();

  if ($ids) {
    $feeds = Feed::loadMultiple($ids);
    foreach ($feeds as $feed) {
      $feed->setQueuedTime(0);
      $feed->save();
    }
  }
}
```
