function **automated_cron_form_system_cron_settings_alter(&$form, &$form_state)**

> Implements hook_form_FORM_ID_alter() for the system_cron_settings() form.

**Code:**
```php
function automated_cron_form_system_cron_settings_alter(&$form, &$form_state) {
  $automated_cron_settings = \Drupal::config('automated_cron.settings');

  // Add automated cron settings.
  $form['automated_cron'] = [
    '#title' => t('Cron settings'),
    '#type' => 'details',
    '#open' => TRUE,
  ];
  $options = [3600, 10800, 21600, 43200, 86400, 604800];
  $form['automated_cron']['interval'] = [
    '#type' => 'select',
    '#title' => t('Run cron every'),
    '#description' => t('More information about setting up scheduled tasks can be found by <a href="@url">reading the cron tutorial on drupal.org</a>.', ['@url' => 'https://www.drupal.org/cron']),
    '#default_value' => $automated_cron_settings->get('interval'),
    '#options' => [0 => t('Never')] + array_map([\Drupal::service('date.formatter'), 'formatInterval'], array_combine($options, $options)),
  ];

  $form['actions']['#type'] = 'actions';
  $form['actions']['submit'] = [
    '#type' => 'submit',
    '#value' => t('Save configuration'),
    '#button_type' => 'primary',
  ];

  // Add submit callback.
  $form['#submit'][] = 'automated_cron_settings_submit';

  // Theme this form as a config form.
  $form['#theme'] = 'system_config_form';
}
```
