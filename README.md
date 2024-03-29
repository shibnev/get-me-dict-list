# getMeDictList

to start type

```
yarn get-langs
```

## Options

All options in file config.js

| name     | default                                                | description                      |
| -------- | ------------------------------------------------------ | -------------------------------- |
| url      | [https://restcountries.com/](https://restcountries.com/) | API url                          |
| fileName | 'data'                                                 | what file name will be on output |
| fileType | 'array'                                                | what type of JSON data will be   |
| template | null                                                   | \* see below                     |

### How to setup template:

This is one of the objects we have in the array:

```
{
  name: 'Afghanistan',
  topLevelDomain: [ '.af' ],
  alpha2Code: 'AF',
  alpha3Code: 'AFG',
  callingCodes: [ '93' ],
  capital: 'Kabul',
  altSpellings: [ 'AF', 'Afġānistān' ],
  region: 'Asia',
  subregion: 'Southern Asia',
  population: 27657145,
  latlng: [ 33, 65 ],
  demonym: 'Afghan',
  area: 652230,
  gini: 27.8,
  timezones: [ 'UTC+04:30' ],
  borders: [ 'IRN', 'PAK', 'TKM', 'UZB', 'TJK', 'CHN' ],
  nativeName: 'افغانستان',
  numericCode: '004',
  currencies: [ { code: 'AFN', name: 'Afghan afghani', symbol: '؋' } ],
  languages: [
    {
      iso639_1: 'ps',
      iso639_2: 'pus',
      name: 'Pashto',
      nativeName: 'پښتو'
    },
    {
      iso639_1: 'uz',
      iso639_2: 'uzb',
      name: 'Uzbek',
      nativeName: 'Oʻzbek'
    },
    {
      iso639_1: 'tk',
      iso639_2: 'tuk',
      name: 'Turkmen',
      nativeName: 'Türkmen'
    }
  ],
  translations: {
    de: 'Afghanistan',
    es: 'Afganistán',
    fr: 'Afghanistan',
    ja: 'アフガニスタン',
    it: 'Afghanistan',
    br: 'Afeganistão',
    pt: 'Afeganistão',
    nl: 'Afghanistan',
    hr: 'Afganistan',
    fa: 'افغانستان'
  },
  flag: 'https://restcountries.eu/data/afg.svg',
  regionalBlocs: [
    {
      acronym: 'SAARC',
      name: 'South Asian Association for Regional Cooperation',
      otherAcronyms: [],
      otherNames: []
    }
  ],
  cioc: 'AFG'
}
```

To customize objects for output, you must set the template settings in file config.js.
Here is an example:

```
export const config = {
  fileName: 'data',
  dataType: 'object',
  template(_this) {
    const countryCode = _this.alpha2Code;
    const nameInEnglish = _this.name;
    const commonLang = _this.languages[0].iso639_1;
    const nativeName = _this.nativeName;
    const currencyCode = _this.currencies ? _this.currencies[0].code : 'USD';
    const currencySymbol = _this.currencies ? _this.currencies[0].symbol : '$';

    return {
      [countryCode]: {
        en: nameInEnglish,
        [commonLang]: nativeName,
        translations: _this.translations,
        currencyCode: currencyCode,
        currencySymbol: currencySymbol
      },
    };
  },
};
```
