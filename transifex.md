# Transifex client

#### Setting source file for new resource
```js
$ tx set --source -r pm-stage-as-test.new_feature -l en as/locale/newfeatures/new_feature.pot
```

#### Push new resource POT file to the new resource
```js
$ tx push -s -r pm-stage-as-test.new_feature
```

#### Pull resource from transifex
```js
$ tx pull -r pm-stage-as.en-source -s
```

#### Pull translated languages from TX
```js
$ tx pull -r pm-stage-as-test.en-source -f
```