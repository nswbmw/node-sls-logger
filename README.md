## ali-sls

The nodejs logger for aliyun SLS with minimum dependencies, forked from [node-sls-logger](https://github.com/innopals/node-sls-logger).

## Installation

```sh
$ npm i ali-sls --save
```

## Configuration

| Config Name  | Default | Type            | Required | Description                                                  |
| ------------ | ------- | --------------- | -------- | ------------------------------------------------------------ |
| accessKey    |         | string          | true     | Your access key to SLS                                       |
| accessSecret |         | string          | true     | Your secret to access SLS                                    |
| endpoint     |         | string          | true     | Your SLS endpoint, e.g. example.cn-hangzhou.log.aliyuncs.com |
| logstore     |         | string          | true     | Your logstore name                                           |
| source       |         | string          | false    | Source for your logs                                         |
| topic        |         | string          | false    | Topic for your logs                                          |
| hashkey      |         | string          | false    |                                                              |
| compress     | false   | boolean         | false    | Use lz4 to compress log payload                              |
| tags         |         | key-value pair  | false    | Extra tags for your logs                                     |
| level        | ALL    | string / number | false    | Log level                                                    |
| disabled     | false   | boolean         | false    | Disable sls and log to stdout                                |

Note: if your configuration is incorrect(fail to get logstore), all logs will be written to stdout.

## Usage

```javascript
const SlsLogger = require('ali-sls')
const slsLogger = new SlsLogger({
  endpoint: "example.cn-hangzhou.log.aliyuncs.com",
  accessKey: "your_access_key",
  accessSecret: "your_access_secret",
  logstore: "your_logstore",
  source: "test",
  topic: "test",
  compress: true,
  level: "INFO",
  disabled: false,
})

slsLogger.info("Hello world!")
slsLogger.log(
  "Hello world!",
  new Date(),
  function () { "abc" },
  { a: 1, b: { c: 1 }, d: "123", e: false },
  new Object(),
  [1, 2, 3, "abc", false, null, undefined, new Error("error1")],
  SlsLogger.createField("module", "main"),
  1234,
  true,
  null,
  undefined
)
slsLogger.error(new Error("error2"))
```
