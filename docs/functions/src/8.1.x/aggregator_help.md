function **aggregator_help($route_name, RouteMatchInterface $route_match)**

> Implements hook_help().

**Code:**
```php
function aggregator_help($route_name, RouteMatchInterface $route_match) {
  switch ($route_name) {
    case 'help.page.aggregator':
      $path_validator = \Drupal::pathValidator();
      $output = '';
      $output .= '<h3>' . t('About') . '</h3>';
      $output .= '<p>' . t('The Aggregator module is an on-site syndicator and news reader that gathers and displays fresh content from RSS-, RDF-, and Atom-based feeds made available across the web. Thousands of sites (particularly news sites and blogs) publish their latest headlines in feeds, using a number of standardized XML-based formats. For more information, see the <a href=":aggregator-module">online documentation for the Aggregator module</a>.', array(':aggregator-module' => 'https://www.drupal.org/documentation/modules/aggregator')) . '</p>';
      $output .= '<h3>' . t('Uses') . '</h3>';
      $output .= '<dl>';
      // Check if the aggregator sources View is enabled.
      if ($url = $path_validator->getUrlIfValid('aggregator/sources')) {
        $output .= '<dt>' . t('Viewing feeds') . '</dt>';
        $output .= '<dd>' . t('Users view feed content in the <a href=":aggregator">main aggregator display</a>, or by <a href=":aggregator-sources">their source</a> (usually via an RSS feed reader). The most recent content in a feed can be displayed as a block through the <a href=":admin-block">Blocks administration page</a>.', array(':aggregator' => \Drupal::url('aggregator.page_last'), ':aggregator-sources' => $url->toString(), ':admin-block' => (\Drupal::moduleHandler()->moduleExists('block')) ? \Drupal::url('block.admin_display') : '#')) . '</dd>';
      }
      $output .= '<dt>' . t('Adding, editing, and deleting feeds') . '</dt>';
      $output .= '<dd>' . t('Administrators can add, edit, and delete feeds, and choose how often to check each feed for newly updated items on the <a href=":feededit">Feed aggregator page</a>.', array(':feededit' => \Drupal::url('aggregator.admin_overview'))) . '</dd>';
      $output .= '<dt>' . t('Configuring the display of feed items') . '</dt>';
      $output .= '<dd>' . t('Administrators can choose how many items are displayed in the listing pages, which HTML tags are allowed in the content of feed items, and whether they should be trimmed to a maximum number of characters on the <a href=":settings">Feed aggregator settings page</a>.', array(':settings' => \Drupal::url('aggregator.admin_settings'))) . '</dd>';
      $output .= '<dt>' . t('Discarding old feed items') . '</dt>';
      $output .= '<dd>' . t('Administrators can choose whether to discard feed items that are older than a specified period of time on the <a href=":settings">Feed aggregator settings page</a>. This requires a correctly configured cron maintenance task (see below).', array(':settings' => \Drupal::url('aggregator.admin_settings'))) . '<dd>';

      $output .= '<dt>' . t('<abbr title="Outline Processor Markup Language">OPML</abbr> integration') . '</dt>';
      // Check if the aggregator opml View is enabled.
      if ($url = $path_validator->getUrlIfValid('aggregator/opml')) {
        $output .= '<dd>' . t('A <a href=":aggregator-opml">machine-readable OPML file</a> of all feeds is available. OPML is an XML-based file format used to share outline-structured information such as a list of RSS feeds. Feeds can also be <a href=":import-opml">imported via an OPML file</a>.', array(':aggregator-opml' => $url->toString(), ':import-opml' => \Drupal::url('aggregator.opml_add'))) . '</dd>';
      }
      $output .= '<dt>' . t('Configuring cron') . '</dt>';
      $output .= '<dd>' . t('A working <a href=":cron">cron maintenance task</a> is required to update feeds automatically.', array(':cron' => \Drupal::url('system.cron_settings'))) . '</dd>';
      $output .= '</dl>';
      return $output;

    case 'aggregator.admin_overview':
      // Don't use placeholders for possibility to change URLs for translators.
      $output = '<p>' . t('Many sites publish their headlines and posts in feeds, using a number of standardized XML-based formats. The aggregator supports <a href="http://en.wikipedia.org/wiki/Rss">RSS</a>, <a href="http://en.wikipedia.org/wiki/Resource_Description_Framework">RDF</a>, and <a href="http://en.wikipedia.org/wiki/Atom_%28standard%29">Atom</a>.') . '</p>';
      $output .= '<p>' . t('Current feeds are listed below, and <a href=":addfeed">new feeds may be added</a>. For each feed, the <em>latest items</em> block may be enabled at the <a href=":block">blocks administration page</a>.', array(':addfeed' => \Drupal::url('aggregator.feed_add'), ':block' => (\Drupal::moduleHandler()->moduleExists('block')) ? \Drupal::url('block.admin_display') : '#')) . '</p>';
      return $output;

    case 'aggregator.feed_add':
      return '<p>' . t('Add a feed in RSS, RDF or Atom format. A feed may only have one entry.') . '</p>';

    case 'aggregator.opml_add':
      return '<p>' . t('<abbr title="Outline Processor Markup Language">OPML</abbr> is an XML format for exchanging feeds between aggregators. A single OPML document may contain many feeds. Aggregator uses this file to import all feeds at once. Upload a file from your computer or enter a URL where the OPML file can be downloaded.') . '</p>';
  }
}
```
