function **ajax_forms_test_advanced_commands_html_callback($form, FormStateInterface $form_state)**

> Ajax form callback: Selects 'html'.

**Code:**
```php
function ajax_forms_test_advanced_commands_html_callback($form, FormStateInterface $form_state) {
  $response = new AjaxResponse();
  $response->addCommand(new HtmlCommand('#html_div', 'replacement text'));
  return $response;
}
```
