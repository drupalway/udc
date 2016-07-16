### Create a form builder class(controller) in src/Forms directory:
```php
/**
 * @file
 * Contains class TestFormDrupalway.
 */

namespace Drupal\my_module\Forms;

use Drupal\Core\Form\FormBase;
use Drupal\Core\Form\FormStateInterface;

/**
 * Class TestFormDrupalway.
 *
 * @package Drupal\my_module\Forms
 */
class TestFormDrupalway extends FormBase {
  public function getFormId() {
    return 'test_form_drupalway';
  }

  public function buildForm(array $form, FormStateInterface $form_state) {
    $form['myform'] = [
      '#type' => 'fieldset',
    ];
    $form['myform']['select'] = [
      '#type' => 'select',
      '#options' => ['option1', 'option2', 'option3'],
      '#title' => 'select',
    ];
    $form['myform']['checkbox'] = [
      '#type' => 'checkbox',
      '#title' => 'checkbox',
    ];
    $form['myform']['text'] = [
      '#type' => 'textfield',
      '#title' => 'textfield',
    ];
    $form['actions'] = [
      'submit' => [
        '#type' => 'submit',
        '#value' => 'Save',
      ],
    ];
    return $form;
  }

  public function validateForm(array &$form, FormStateInterface $form_state) {
    if ($form_state->getValue('select') != 0) {
      $form_state->setErrorByName('select', 'WRONG DROPDOWN VALUE');
    }
    parent::validateForm($form, $form_state);
  }

  public function submitForm(array &$form, FormStateInterface $form_state) {
    $form_state->setRebuild();
    foreach ($form_state->getValues() as $key => $value) {
      drupal_set_message($key . ': ' . $value);
    }
  }

}
```