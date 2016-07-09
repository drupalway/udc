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

> * **$arg1**:
    type: _array_
    description:
      _Argument 1 description._
> * **$arg2**:
    type: _string_
    default: NULL
    description:
      _Argument 2 description._

> * **return**:
    type: _object_
    description:
      _Return some object._

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
