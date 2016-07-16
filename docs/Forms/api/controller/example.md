## Create a form builder class(controller) in src/Forms directory:
To create a form builder class you have to create a new file in src/Forms directory, let's call it "TestFormDrupalway.php".
Next step is that your own class could be extended from the FormBase class.
```php
class TestFormDrupalway extends FormBase {
}
```
Now we have to specify a required methods specified in FormInterface interface.
They are: getFormId(), buildForm() and submitForm().

### getFormId
In getFormId() method we have to specify our form ID.
```php
public function getFormId() {
  return 'test_form_drupalway';
}
```
### buildForm
The buildForm() method allows us to build a render-able array.
```php
public function buildForm(array $form, FormStateInterface $form_state) {
  $form['myform'] = [
    '#type' => 'fieldset',
  ];
  $form['myform']['select'] = [
    '#type' => 'select',
    '#options' => ['option1', 'option2', 'option3'],
    '#title' => $this->t('My own select'),
  ];
  $form['myform']['checkbox'] = [
    '#type' => 'checkbox',
    '#title' => $this->t('My own checkbox'),
  ];
  $form['myform']['text'] = [
    '#type' => 'textfield',
    '#title' => $this->t('My own textfield'),
  ];
  $form['actions'] = [
    'submit' => [
      '#type' => 'submit',
      '#value' => $this->t('Submit this form'),
    ],
  ];
  return $form;
}
```
### validateForm
Optionally you can add your own validation method for this thing.
```php
public function validateForm(array &$form, FormStateInterface $form_state) {
  if ($form_state->getValue('select') != 0) {
    $form_state->setErrorByName('select', 'WRONG DROPDOWN VALUE');
  }
  parent::validateForm($form, $form_state);
}
```
### submitForm
The final part is adding a submission method
```php
public function submitForm(array &$form, FormStateInterface $form_state) {
  foreach ($form_state->getValues() as $key => $value) {
    drupal_set_message($key . ': ' . $value);
  }
}
```

### Full example:
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