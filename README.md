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

after changing the `metaData` class exposes items with the property `type` together with the existing `name` (I use [lodash](https://lodash.com/docs)):
```javascript
connection.execute(
  "SQL statement",
  [],
  function(err, result)
  {
    var columns = _.map(result.metaData, function(data){
      return {
        fieldName: data.name,
        dataType: data.type
      };
    });
  });
```

# Data Types #
on line `1772` of the file `njsConnection.cpp` you can read data types converter.

return data types (js style):
- string
- number
- integer
- date
- object


to change or expand the data types list edit the file and rebuild.
