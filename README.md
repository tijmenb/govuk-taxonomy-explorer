# GOV.UK Taxonomy explorer

This is a visualisation of GOV.UK's single subject taxonomy.

<https://github.com/alphagov/govuk-taxonomy-explorer>

## Regenerating the data

```
bundle exec rake generate_network
```

## Limitations

The root taxons are currently hard coded. We should be able to get them from the content-store.
