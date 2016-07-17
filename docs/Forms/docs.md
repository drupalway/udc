Form API
========

Form workflow usually follows these stages:

* Declaration of a form and its elements in a function
* Modification of existing forms with the FAPI hook system
* Theming of forms
* Form validation and submission

Forms are represented as arrays in form builder functions.
 Each item within the $form array on api.drupal.org corresponds either
 to a form element (an input or other HTML on the rendered form)
 or an element property (meta-data used by FAPI during the rendering or processing of elements).
 A property has a key name that begins with a "#", while an element does not.
 
The Drupal 8 Form API is largely similar to the Drupal 7 Form API.
 The forms are still represented with nested render array structures
 and there is a separate validation and submission step.
 There are some new (HTML 5) elements available and the integration of these components
 into the rest of the Drupal system changed a bit.

In Drupal 8, Forms are defined by implementing the \Drupal\Core\Form\FormBuilderInterface
 and the basic workflow of a form is defined by
 buildForm, validateForm, and submitForm methods on the interface.


# New Form API HTML5 elements in Drupal 8
There are new HTML 5 elements like
 - '#type' => 'tel'
 - '#type' => 'email'
 - '#type' => 'number'
 - '#type' => 'date'
 - '#type' => 'url'
 - '#type' => 'search'
 - '#type' => 'range'
 - etc.
Using these elements as opposed to requesting data in plain textfields is preferable
because devices can pull up the proper input methods for them,
such as when a telephone number is requested, the dialpad would show up on a device.

There are also other elements added to help structure your forms.
The '#type' => 'details' element is a grouping element with a summary.
The '#type' => 'language_select' element is a language selector to make it easy
to put language configuration on forms. The '#type' => 'dropbutton' and '#type' => 'operations'
elements are the dropdown link/operations list that you may know from Views,
now used consistently for operations in Drupal 8.

# Drupal 8 overview
Form classes implement the \Drupal\Core\Form\FormBuilderInterface and the basic workflow of a form is defined by the buildForm, validateForm, and submitForm methods of the interface. When a form is requested it's defined as a renderable array often referred to as a Form API array or simply $form array. The $form array is converted to HTML by the render process and displayed to the end user. When a user submits a form the request is made to the same URL that the form was displayed on, Drupal notices the incoming HTTP POST data in the request and this time instead of building the form and displaying it as HTML builds the form and then proceeds to call the applicable validation and submission handlers.

Defining forms as structured arrays instead of straight HTML has many advantages including:
- Consistent HTML output for all forms.
- Forms provided by one module can be easily altered by another without complex search and replace logic.
- Complex form elements like file uploads and voting widgets can be encapsulated in reusable bundles that include both display and processing logic.
 
## Form builder.

To create a form we might have to create some form builder functionality.

In Drupal 7 it was a function, like the following one:
```php
/**
 *  Form constructor for the example form.
 */
function mymodule_example_form($form, &$form_state) {
  // Provide a text field.
  $form['name'] = array(
    '#title' => t('Your full name'),
    '#type' => 'textfield',
    '#required' => TRUE,
  );
  
  // Provide a submit button.
  $form['submit'] = array(
    '#type' => 'submit',
    '#value' => 'Update search',
  );
  
  return $form;
}
```
In Drupal 8 this is represented as the special class, extended from the FormBase class
 and should contain the following methods, described in FormInterface:
- **getFormId.** This needs to return a string that is the unique ID of your form.
- **buildForm.** Which returns a Form API array that defines each of the elements your form is composed of.
- **validateForm(optional).** Optional method for validating the form.
- **submitForm.** Form submission handler.

```php
class ExampleForm extends FormBase {
  public function getFormId() {
    return 'example_form';
  }
  public function buildForm(array $form, FormStateInterface $form_state) {
    $form['phone_number'] = array(
      '#type' => 'tel',
      '#title' => $this->t('Your phone number'),
    );
    $form['actions']['#type'] = 'actions';
    $form['actions']['submit'] = array(
      '#type' => 'submit',
      '#value' => $this->t('Save'),
      '#button_type' => 'primary',
    );
    return $form;
  }
  public function validateForm(array &$form, FormStateInterface $form_state) {
    if (strlen($form_state->getValue('phone_number')) < 3) {
      $form_state->setErrorByName('phone_number', $this->t('The phone number is too short. Please enter a full phone number.'));
    }
  }
  public function submitForm(array &$form, FormStateInterface $form_state) {
    drupal_set_message($this->t('Your phone number is @number', array('@number' => $form_state->getValue('phone_number'))));
  }
}
```

## Integrate the form in a request
In Drupal 7 it was can be implemented via some menu route entries in hook_menu():
```php
/**
 * Implements hook_menu().
 */
function mymodule_menu() {
  $items = array();
  $items['mymodule/test_form'] = array(
    'title'            => 'Test form',
    'page callback'    => 'drupal_get_form',
    'page arguments'   => array('mymodule_test_form'),
    'access callback'  => TRUE,
    'file'             => 'mymodule.form.inc',
    'type'             => MENU_NORMAL_ITEM,
  );
  return $items;
}
```
Drupal 8 usual flow for creating a menu routes - *.routing.yml files, so we can do the following:
```yml
mymodule.test_form:
  path: 'mymodule/test_form'
  defaults:
    _form: '\Drupal\mymodule\Forms\ExampleForm'
    _title: 'Test form'
  requirements:
    _permission: 'access content'
```
## Retrieving this form outside of routes
In Drupal 7 we have a function ```drupal_get_form()``` for this.
Although Drupal 7's drupal_get_form() is gone in Drupal 8,
 there is a FormBuilder service that can be used to retrieve and process forms.
 The Drupal 8 equivalent of drupal_get_form() is the following:
```php
$form = \Drupal::formBuilder()->getForm('Drupal\example\Form\ExampleForm');
```
The argument passed to the getForm() method is the name of the class that defines your form
 and is an implementation of \Drupal\Core\Form\FormBuilderInterface.
 If you need to pass any additional parameters to the form, pass them on after the class name.
 
# Altering form
Altering forms is where the Drupal 8 Form API reaches into basically the same approach where Drupal 7 is.
 Given that you provided a form ID for your form, altering is based on that.
 Use hook_form_alter() and/or hook_form_FORM_ID_alter() to alter the form.
 One small point that for D8 the arguments of that hook is a bit different,
 usually $form is restricted to the array type and the $form_state is now an instance of the FormStateInterface.
 
### D7:
```php
/**
 * Implements hook_form_FORM_ID_alter().
 */
function example2_form_example_form_alter(&$form, &$form_state) {
  $form['phone_number']['#description'] = t('Start with + and your country code.');
}
```
### D8:
```php
/**
 * Implements hook_form_FORM_ID_alter().
 */
function example2_form_example_form_alter(array &$form, FormStateInterface $form_state) {
  $form['phone_number']['#description'] = t('Start with + and your country code.');
}
```
