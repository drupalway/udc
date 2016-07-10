function **automated_cron_help($route_name, RouteMatchInterface $route_match)**

> Implements hook_help().

**Code:**
```php
function automated_cron_help($route_name, RouteMatchInterface $route_match) {
  switch ($route_name) {
    case 'help.page.automated_cron':
      $output = '';
      $output .= '<h3>' . t('About') . '</h3>';
      $output .= '<p>' . t('The Automated Cron module runs cron operations for your site using normal browser/page requests instead of having to set up a separate cron job. The Automated Cron module checks at the end of each server response when cron operation was last ran and, if it has been too long since last run, it executes the cron tasks after sending a server response. For more information, see the <a href=":automated_cron-documentation">online documentation for the Automated Cron module</a>.', [':automated_cron-documentation' => 'https://www.drupal.org/documentation/modules/automated_cron']) . '</p>';
      $output .= '<h3>' . t('Uses') . '</h3>';
      $output .= '<dl>';
      $output .= '<dt>' . t('Configuring Automated Cron') . '</dt>';
      $output .= '<dd>' . t('On the <a href=":cron-settings">Cron page</a>, you can set the frequency (time interval) for running cron jobs.', [':cron-settings' => \Drupal::url('system.cron_settings')]) . '</dd>';
      $output .= '<dt>' . t('Disabling Automated Cron') . '</dt>';
      $output .= '<dd>' . t('To disable automated cron, the recommended method is to uninstall the module, to reduce site overhead. If you only want to disable it temporarily, you can set the frequency to Never on the Cron page, and then change the frequency back when you want to start it up again.') . '</dd>';
      $output .= '</dl>';
      return $output;
  }
}
```
