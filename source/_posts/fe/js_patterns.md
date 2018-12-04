---
title: javscript-patterns-设计模式
categories: FE
tags:
- js 设计模式
- javascript
comments: true
---

## 单例模式

```js
class Apple {
    constructor(name, creator, products) {
        if (!Apple.instance) {
            this.name = name
            this.creator = creator
            this.products = products
            Apple.instance = this
        }
        return Apple.instance;
    }
}
// let appleCompany = new Apple('苹果公司', '乔布斯', ['iphone', 'imac', 'ipad'])
// 优化版
class Apple1 {
    constructor(name, creator, products) {
        this.name = name
        this.creator = creator
        this.products = products
    }

    static create(name, creator, products) {
        if (!Apple1.instance) {
            Apple1.instance = new Apple1(name, creator, products);
        }
        return Apple1.instance;
    }
}

let copyCompany = Apple1.create('苹果公司', '乔布斯', ['iphone', 'imac', 'ipad'])
let copyCompany1 = Apple1.create('苹果公司1', '乔布斯1', ['iphone1', 'imac1', 'ipad1'])
console.log(copyCompany1)
```

## 策略模式

```js
// 策略模式 可以做统一表单验证

let data = new Map([['first_name', 'Super'], ['last_name', 'Man'], ['age', 'unknown'], ['username', 'o_0']]);
let config = new Map([['first_name', 'isNonEmpty'], ['age', 'isNumber'], ['username', 'isAlphaNum']]);

// 校验规则类
class Checker {
    constructor(check, instructions) {
      [this.check, this.instructions] = [check, instructions];
    }
}

class Validator {
    constructor(config) {
      [this.config, this.messages] = [config, []];
    }
  
    validate(data) {
      // 对map遍历
      for (let [k, v] of data.entries()) {
        // 获取每个值
        let type = this.config.get(k);
        // 获取规则函数
        let checker = Validator[type];
        // 如果没有值 跳出本次循环
        if (!type) continue;
        // 如果校验不公国 报错
        if (!checker) throw new Error(`No handler to validate type ${type}`);
        // 使用本次规则校验本次数据
        let result = checker.check(v);
        // 记录日志
        if (!result) this.messages.push(checker.instructions + ` **${v}**`);
      }
    }
  
    hasError() {
      return this.messages.length !== 0;
    }
}

                                 // 前面是一个函数 后面是字符串
Validator.isNumber = new Checker((val) => !isNaN(val), 'the value can only be a valid number');
Validator.isNonEmpty = new Checker((val) => val !== "", 'the value can not be empty');
Validator.isAlphaNum = new Checker((val) => !/^a-z0-9/i.test(val), 'the value can not have special symbols');

let validator = new Validator(config);
validator.validate(data);
console.log(validator.messages.join('\n')); // the value can only be a valid number **unknown**
```


## 代理模式

```js
class SeaName {
    // 构造函数
    constructor(name){
        this.name = name
    }
    sea () {
        console.log('我的名字叫' + this.name)
    }
}

class ProxySeaName extends SeaName {
    constructor () {
        // 继承构造函数
        super(...arguments);
    }
    sea () {
        // 这里需要矫正this指向
        setTimeout(super.sea.bind(this), 3 * 1000)
    }
}

let nameClass = new ProxySeaName('lishi1');
console.log(nameClass.name)
nameClass.sea()
```