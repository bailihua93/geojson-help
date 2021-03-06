# geojson-help

>command line for the GeoJSON format and encode

[![node](https://img.shields.io/node/v/geojson-help.svg?style=flat-square)](https://www.npmjs.com/package/geojson-help)
[![npm](https://img.shields.io/npm/dw/geojson-help.svg?style=flat-square)](https://www.npmjs.com/package/geojson-help)

## 安装

```
$ npm install geojson-help -g
```

## 使用

#### 1. 格式转换

```bash
$ geo format  -i <input>
```

- 默认将`arcgis-json`插件导出的json文件转换成标准`geojson`格式，后续扩展其它途径的转换
- `-i`参数为需要被转换的json文件的路径，支持[glob](https://github.com/isaacs/node-glob)匹配
- 默认输出转换后的文件到`json_geo`文件夹下，文件名保持不变

示例：

```bash
$ geo format -i "json/*.json"
```

*注意：-i osx系统，参数值必须为[双引号](https://www.npmjs.com/package/geojson-help)包裹的字符串，未加双引号路径会被预先解析，只能匹配到一个结果；windows下可加可不加，但是别使用单引号，匹配不到的。具体原因不明，有了解的麻烦告诉我。*

#### 2. 压缩

使用字符集编码转换和`ZigZag`算法压缩标准`geosjon`的几何数据，文件末尾用`"UTF8Encoding": true`作为标示。结果适用于[echarts](http://echarts.baidu.com/)。也可结合`decode`解码方法，应用于支持`geojson`的地图，如[leaflet](http://leafletjs.com/)

```bash
$ geo encode -i <input>
```

- 参数说明同上
- 转换后输出到`json_geo_encode`文件夹下

示例：

```bash
$ geo encode -i "json_geo/*.json"
```

#### 3. 解码

针对`2.`的压缩结果做解码，还原成标准`geojson`数据。压缩-还原过程，会导致经纬度精度丢失，但一般不影响图层显示。

```bash
$ geo decode -i <input>
```

#### 4.格式化&压缩

连续操作格式化和压缩，其它同上

```bash
$ geo transform -i <input>
```

## API

也提供了api接口供运行环境使用

```bash
# 安装到项目
npm i geojson-help --save
```

示例：

```js
import geo from 'geojson-help'
import arcgisjson from '../assets/arcgisjson.json'

var geojson = geo.format(arcgisjson)
var geojsonEncode = geo.encode(geojson)
var geojsonDecode = geo.decode(geojsonEncode)
```

## 测试demo

1. `clone` 源码到本地， 到该目录执行`npm run dev`， 打开`localhost:9090/demo/index.html`， 修改`index.html`中`render`函数的geojson文件引用，可看结果。
2. 将文件导入到[mapshaper](http://mapshaper.org/)验证。

## 待扩展

1. 压缩解码缩放参数
2. 'format'精度控制，拐点抽稀，进一步提高压缩比。

[欢迎提issue](https://github.com/lefreet/geojson-help/issues)



