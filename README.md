# Activate return data types on oracledb module

### waiting for fix [issue](https://github.com/oracle/node-oracledb/issues/358) and without any pretense of breaking the terms of the original license, you can use this procedure to perform tests ###

copy all files (**.cpp**, **.h**) in folder (*overwriting the originals*):
```sh
../node_modules/oracledb/src/njs/src
```

move on path:
```sh
$ cd node_modules/oracledb
```

execute:
```sh
$ node-gyp rebuild
```

# Retrieve Data Types in MetaData #

after changing the `metaData` array exposes items with more properties:

- `name` : field name
- `type` : field data type (JS datatype)
- `originalType` : field data type (DB datatype)
- `size` : DB field size
- `precision` : DB field precision
- `scale` : DB field scale
- `isNullable` : field can be null

```javascript
connection.execute(
  "... SQL statement ...",
  [],
  function(err, result)
  {
    var columns = _.map(result.metaData, function(c)
    {
      return {
        name: c.name || '',
        type: c.type || '',
        originalType: c.originalType || 'undefined',
        size: c.size || 0,
        precision: c.precision || 0,
        scale: c.scale || 0,
        isNullable: c.isNullable
      };
    });
  });
```
(I use [lodash](https://lodash.com/docs)):


# Data Types #
on line `1764` of the file `njsConnection.cpp` you can read data types (JS) converter.

return data types (js datatype):
- string
- number
- date
- object


to change or expand the data types list edit the file and rebuild.
