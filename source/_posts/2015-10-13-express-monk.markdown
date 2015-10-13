---
layout: post
title: "express Mongodb"
date: 2015-10-13 11:44
comments: true
categories: []
---

最近在学习用Nodejs的express和mongodb学习，具体可以参考http://cwbuecheler.com/web/tutorials/2013/node-express-mongo/ 这个有比较详细的讲解，但在使用中会发现报找不到bson这个模块的错误。

具体报错如下：
···
{ [Error: Cannot find module '../build/Release/bson'] code: 'MODULE_NOT_FOUND' }
js-bson: Failed to load c++ bson extension, using pure JS version
···

主要原因，是bson的c++版本扩展没有找到，因此它会建议你使用js的bson版本。使用bson之前版本是在mongodb的npm中使用，但后来则在monk上使用。

## 如何切换到js的bson呢？

- 首先在node_modules中的monk里的mongodb中的进行npm install 一下。
- 其次你需要修改一下`./monk/node_modules/mongodb/node_modules/bson/ext/index.js`中第10行和第16行进行修改。

```javascript
var bson = null;

try {
	// Load the precompiled win32 binary
	if(process.platform == "win32" && process.arch == "x64") {
	  bson = require('./win32/x64/bson');  
	} else if(process.platform == "win32" && process.arch == "ia32") {
	  bson = require('./win32/ia32/bson');  
	} else {
		bson = require('../browser_build/bson');  
	  	// bson = require('../build/Release/bson');  
	}	
} catch(err) {
	// Attempt to load the release bson version
	try {
		bson = require('../browser_build/bson');
		// bson = require('../build/Release/bson');
	} catch (err) {
		console.dir(err)
		console.error("js-bson: Failed to load c++ bson extension, using pure JS version");
		bson = require('../lib/bson/bson');
	}
}
```

这样就可以了，很简单。