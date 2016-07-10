function **archiver_get_extensions()**

> Returns a string of supported archive extensions.

* **Return:**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;type: _string_
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;description: _A space-separated string of extensions suitable for use by the file validation system._

**Code:**
```php
function archiver_get_extensions() {
  $valid_extensions = array();
  foreach (\Drupal::service('plugin.manager.archiver')->getDefinitions() as $archive) {
    foreach ($archive['extensions'] as $extension) {
      foreach (explode('.', $extension) as $part) {
        if (!in_array($part, $valid_extensions)) {
          $valid_extensions[] = $part;
        }
      }
    }
  }
  return implode(' ', $valid_extensions);
}
```
