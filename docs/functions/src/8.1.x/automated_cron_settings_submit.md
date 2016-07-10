function **automated_cron_settings_submit(array $form, FormStateInterface $form_state)**

> Form submission handler for system_cron_settings().

**Code:**
```php
function automated_cron_settings_submit(array $form, FormStateInterface $form_state) {
  \Drupal::configFactory()->getEditable('automated_cron.settings')
    ->set('interval', $form_state->getValue('interval'))
    ->save();
  drupal_set_message(t('The configuration options have been saved.'));
}
```
