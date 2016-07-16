### Override the form via class extending:
```php
/**
 * @file
 * Class TestFormDrupalwayAlter.
 */

namespace Drupal\my_module\Forms;

use Drupal\Core\Form\FormStateInterface;

/**
 * Class TestFormDrupalwayAlter.
 *
 * @package Drupal\my_module\Forms
 */
class TestFormDrupalwayAlter extends TestFormDrupalway {
  public function buildForm(array $form, FormStateInterface $form_state) {
    $form = parent::buildForm($form, $form_state);
    // Do whatever you want with a form array.
    return $form;
  }
  public function validateForm(array &$form, FormStateInterface $form_state) {
    // Add your own validation code here.
    parent::validateForm($form, $form_state);
  }
  public function submitForm(array &$form, FormStateInterface $form_state) {
    parent::submitForm($form, $form_state);
    // Add your own submission code here.
  }

}

```