---
layout: post
read_time: true
show_date: true
title:  types/uuid - Uncaught TypeError Object(...) is not a function
date:   2021-12-30 08:00:00 +0100
description: types/uuid - Uncaught TypeError Object(...) is not a function, Universally Unique Identifier, GUID
img: posts/uncategorized/reactjs.png
tags: [ReactJS]
author: SUN Jiangong
canonical_url: 'https://www.sunjiangong.com/types-uuid-uncaught-type-error-object-is-not-a-function.html'
---

If you want to check if a string is an UUID (Universally Unique Identifier, aka GUID) in reactjs.

You can use the NPM package [@types/uuid](https://yarnpkg.com/package/@types/uuid){:target='_blank'} to do it.

<!--more-->
<br/>

Here I created a helper class to validate a string.

```javascript
import { validate as uuidValidate } from 'uuid';

export class StringUtils {
    static isValidUuid = (identifier: string) => {
        return uuidValidate(identifier);
    }
}
```

<br/>

But I've encountered the following error:

```bat
Uncaught TypeError: Object(...) is not a function
    at Function.Bc.isValidUuid (VM97 main.5b67c597.chunk.js:17)
```

To fix it, I have to install the npm package [uuid](https://yarnpkg.com/package/uuid){:target='_blank'}. As it has a dependency on it.

```bat
yarn add uuid
```
or 
```bat
npm install uuid --save
```

