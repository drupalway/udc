function **archiver_get_archiver($file)**

> Creates the appropriate archiver for the specified file.

* **$file**:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;type: _mixed_
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;description: _The full path of the archive file. Note that stream wrapper paths are supported, but not remote ones._

* **Return:**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;type: _object|bool_
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;description: _A newly created instance of the archiver class appropriate for the specified file, already bound to that file. If no appropriate archiver class was found, will return FALSE._

**Code:**
```php
function archiver_get_archiver($file) {
  // Archivers can only work on local paths
  $filepath = drupal_realpath($file);
  if (!is_file($filepath)) {
    throw new Exception(t('Archivers can only operate on local files: %file not supported', array('%file' => $file)));
  }
  return \Drupal::service('plugin.manager.archiver')->getInstance(array('filepath' => $filepath));
}
```
