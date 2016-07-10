function **ajax_forms_test_advanced_commands_css_callback($form, FormStateInterface $form_state)**

> Ajax form callback: Selects 'css'.

**Code:**
```php
function ajax_forms_test_advanced_commands_css_callback($form, FormStateInterface $form_state) {
  $selector = '#css_div';
  $color = 'blue';

  $response = new AjaxResponse();
  $response->addCommand(new CssCommand($selector, array('background-color' => $color)));
  return $response;
}
```
