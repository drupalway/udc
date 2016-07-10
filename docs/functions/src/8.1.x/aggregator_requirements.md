function **aggregator_requirements($phase)**

> Implements hook_requirements().

**Code:**
```php
function aggregator_requirements($phase) {
  $has_curl = function_exists('curl_init');
  $requirements = array();
  $requirements['curl'] = array(
    'title' => t('cURL'),
    'value' => $has_curl ? t('Enabled') : t('Not found'),
  );
  if (!$has_curl) {
    $requirements['curl']['severity'] = REQUIREMENT_ERROR;
    $requirements['curl']['description'] = t('The Aggregator module could not be installed because the PHP <a href="http://php.net/manual/curl.setup.php">cURL</a> library is not available.');
  }
  return $requirements;
}
```
