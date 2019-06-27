# secretKeyUtil

```js
'use strict';

/**
 * @util runtime时匹配密钥的工具,从高版本到低版本匹配
 */

function secretKeyUtil(config, vid, cryptType) {
    // 1 匹配vid
    let isExist = Object.keys(config).includes(vid);

    // 2 是否存在？
    if (isExist) {
        return config[vid][cryptType];
    }

    // 3 未匹配到密钥，找最近的
    let sortArr = Object.keys(config).sort((a, b) => b - a);

    for (let cvid of sortArr) {
        if (+vid >= +cvid) {
            return config[cvid][cryptType];
        }
    }

    // 4 如果再找不到 使用default
    return config['default'][cryptType];
}

module.exports = secretKeyUtil;


```
