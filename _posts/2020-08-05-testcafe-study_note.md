---
layout: post
title:  "TestCafe 快速上手 - 待完善"
date:   2020-08-05 22:00:00 +0800
categories: JavaScript
tags: JavaScript
---

# Run test
## 一.命令行
### 选项
1.--test-meta , --fixture-meta
* 根据元数据过滤测试用例

## 二.Runner
### 1.filter
```
runner.filter((testName, fixtureName, fixturePath, testMeta, fixtureMeta) => {
    return fixturePath.startsWith('D') &&
        testName.match(someRe) &&
        fixtureName.match(anotherRe) &&
        testMeta.mobile === 'true' &&
        fixtureMeta.env === 'staging';
});
```

## 三.Skip Tests
### 1.fixture.skip and test.skip
* 跳过指定用例

example
```
fixture.skip `Fixture 1`; // All tests in this fixture are skipped

test('Fixture 1 - Test 1', () => {});
test('Fixture 1 - Test 2', () => {});

fixture `Fixture 2`;

test('Fixture 2 - Test 1', () => {});
test.skip('Fixture 2 - Test 2', () => {}); // This test is skipped
test('Fixture 2 - Test 3', () => {});
```
### 2.fixtrue.only and test.only
* 只执行指定用例

example
```
fixture.only `Fixture 1`;
test('Fixture 1 - Test 1', () => {});
test('Fixture 1 - Test 2', () => {});

fixture `Fixture 2`;

test('Fixture 2 - Test 1', () => {});
test.only('Fixture 2 - Test 2', () => {});
test('Fixture 2 - Test 3', () => {});

// Only tests in 'Fixture 1' and the 'Fixture 2 - Test 2' test are run
```
思考： 是否可以写明跳过的条件和原因？

# Report
## 1.自定义测试报告
### 安装依赖
```
npm install -g yo
npm install -g generator-testcafe-reporter
```
### 创建报告文件夹
```
mkdir my-reporter
cd my-reporter
```
## 2.显示测试用例元数据meta

# Fixtures
## 1.声明fixtures

## 2.打开网页
```
fixture 'myfixture'
   .page 'http://www.baidu.com';
```

## 3.指定测试元数据
相当于pytest.mark
```
fixture `My fixture`
    .meta('fixtureID', 'f-0001')
    .meta({ author: 'John', creationDate: '05/03/2018' });
```
# Initialization and Clean-Up 初始化和清理
* 指定函数在fixture之前/测试用例执行之前或之后运行，这些函数被称为hooks.
## Test Hooks
* 测试用例级别的fixture
### 1.fixture.beforeEach and fixture.afterEach
* 为每一个测试用例声明hooks
example
```
fixture `My fixture`
    .page `http://example.com`
    .beforeEach( async t => {
        await t
            .useRole(admin)
            .click('#open-management-console');
    })
    .afterEach( async t => {
        await t.click('#delete-data');
    });
```
### 2.test.before and test.after
* 为指定测试用例指定hooks,当声明了before 或者 after, 对应的fixture.beforeEach and fixture.afterEach 将被覆盖，且不执行。
example
```
test
    .before( async t => {
        await t
            .useRole(admin)
            .click('#open-management-console');
    })
    ('MyTest', async t => { /* ... */ })
    .after( async t => {
        await t.click('#delete-data');
    });
```
## Fixture Hooks
* 在第一个用例之前执行 或者 在最后一个用例之后执行
1.fixture.before and fixture.afte
example
```
fixture `My fixture`
    .page `http://example.com`
    .before( async ctx => {
        utils.populateDb(ctx.dbName);
    })
    .after( async ctx => {
        utils.dropDb(ctx.dbName);
    });
```
## 如何在hooks 和测试用例之间共享数据?

# 测试用例
## 1.声明测试用例
```
test('test1',async t=>{
  /*test code*/
  });
```
## 2.每个用例打开指定页面
### test.page
```
test1
     .page 'http://devexpress.github.io/'
     ('test1',async t=>{
       /*test code*/
      });
```

## 3.指定测试元数据
相当于pytest.mark
```
test
    .meta('testID', 't-0005')
    .meta({ severity: 'critical', testedAPIVersion: '1.0' })
    ('MyTest', async t => { /* ... */});
```

# Select Page Elements
## 1.member tables
源码：<a href="https://github.com/DevExpress/testcafe/blob/master/src/client-functions/selectors/add-api.js" target="_blank"> addFilterMethods</a>

Method|Description
:--:|:--:
nth|Finds an element by its index.
withText|Finds an element whose content includes the specified text.
withExactText|Finds an element with the specified text.
withAttribute|Finds an element with the specified attribute or attribute value.
filterVisible|Selects visible elements.
filterHidden|Selects hidden elements.
filter|Finds elements that match the specified CSS selector or predicate.
find|Finds a descendant node that matches the specified CSS selector or predicate.
parent|Selects parent elements.
child|Selects child elements.
sibling|Selects sibling elements.
nextSibling|Selects succeeding sibling elements.
prevSibling|Selects preceding sibling elements.

## 2.Use Selectors
### 1. 检查元素是否存在 exists
example
`
Selector('#submit-button').exists;
`
### 2.显示匹配的数量 count
example
`
Selector('.column.col-2 label').count;
`
### 3.获取元素节点状态  Obtain Element State
<a href="https://devexpress.github.io/testcafe/documentation/reference/test-api/domnodestate.html" target="_blank"> DOMNodeState API reference</a>

如获取元素ID，attributes等；

**注意： 这些方法和属性是异步的，所以在使用之前使用await**



[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help