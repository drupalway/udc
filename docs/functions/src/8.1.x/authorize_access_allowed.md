function **authorize_access_allowed(Request $request)**

> Determines if the current user is allowed to run authorize.php.

> The killswitch in settings.php overrides all else, otherwise, the user must have access to the 'administer software updates' permission.

* **$request:**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;type: _\Symfony\Component\HttpFoundation\Request_
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;description: _The incoming request._

* **Return:**
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;type: _bool_
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;description: _TRUE if the current user can run authorize.php, and FALSE if not._

**Code:**
```php
function authorize_access_allowed(Request $request) {
  $account = \Drupal::service('authentication')->authenticate($request);
  if ($account) {
    \Drupal::currentUser()->setAccount($account);
  }
  return Settings::get('allow_authorize_operations', TRUE) && \Drupal::currentUser()->hasPermission('administer software updates');
}
```