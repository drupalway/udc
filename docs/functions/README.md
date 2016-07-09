Template for functions.
=======================
### Document structure:
1. Signature
2. Short description
3. Long description(if exists)
4. Arguments description
5. Return statement description(if returns something)
6. Code

### Example:

function **my_function(array $arg1, $arg2 = NULL)**

> This function allow users(short description)....

> Additional info for this function(long description).

* **$arg1**:\
&nbsp;&nbsp;&nbsp;&nbsp;type: _array_\
&nbsp;&nbsp;&nbsp;&nbsp;description: _Argument 1 description._
* **$arg2**:\
&nbsp;&nbsp;&nbsp;&nbsp;type: _string_\
&nbsp;&nbsp;&nbsp;&nbsp;default: _NULL_\
&nbsp;&nbsp;&nbsp;&nbsp;description: _Argument 2 description._

* **return**:\
&nbsp;&nbsp;&nbsp;&nbsp;type: _object_\
&nbsp;&nbsp;&nbsp;&nbsp;description: _Return some object._

**Code:**
```php
function my_function(array $arg1, $arg2 = NULL) {
  $object = new stdClass();
  foreach($arg1 as $name => $value) {
    $object->{$name} = $value;
  }
  if (!empty($arg2)) {
    $object->arg = $arg2;
  }
  return $object;
}
```
