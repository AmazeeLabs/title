# Title

A Drupal module forked from https://www.drupal.org/project/title 7.x-1.x branch (dev).

## Differences from contrib version

- There are bugfixes we need that are really special, so they won't be committed to contrib module.
- Reverse synchronization is disabled.  
  Reverse synchronization copied value of legacy field to regular field. For example from `$entity->title` to `$entity->title_field[$langcode][0]['value']`.  
  This was disabled because
    - we don't have cases when the legacy field can be changed advisedly,
    - it can bring bugs.

## Behaviour rules

- On entity load: set `$entity->legacy_field` from `$entity->regular_field[{current-content-langcode}][0]['value']` (so the `$entity->legacy_field` is displayed correctly on the page, etc)
- On entity save: set `$entity->legacy_field` from `$entity->regular_field[{entity-original-language}][0]['value']` (so, the `$entity->legacy_field` is stored in the database in the entity original language)

## Tests

Currently module tests fail because reverse synchronization is disabled.
