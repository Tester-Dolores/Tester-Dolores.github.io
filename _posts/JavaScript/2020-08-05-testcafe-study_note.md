---
layout: post
title:  TestCafe 快速上手 - 待完善
category: JavaScript
tags: [ui自动化测试]
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

# 截屏 screenshots
## 测试用例执行失败时截屏
1.命令行

testcafe chrome ./ **-s takeOnFails=true**

2.runner.screenshots
```
runner.screenshots({
  takeOnFails:true
  });
```
3.配置文件
```
{
  "screenshots":{
    "takeOnFails":true
  }
}
```

## 截屏选项
Option|Type|Description|Default Value
:--:|:--:|:--:|:--:
path|String	|The base directory where screenshots are saved.	|./screenshots
takeOnFails|	Boolean|	true to take a screenshot whenever a test fails.	|false
pathPattern	|String	|A pattern that defines how TestCafe composes the relative path to a screenshot file. See Screenshot and Video Directories.	|See Default Path Pattern.
fullPage	|String	|true to capture the full page, including content that is not visible due to overflow.	|false

## 截图文件名自定义参数
Placeholder|Description
:--:|:--:
${DATE}	|测试开始日期
${TIME}	|测试开始时间
${TEST_INDEX}	|The test's index.
${FILE_INDEX}	|The screenshot file's index.
${QUARANTINE_ATTEMPT}	|The quarantine attempt's number. If the quarantine mode is disabled, the ${QUARANTINE_ATTEMPT}| placeholder's value is 1.
${FIXTURE}	|The fixture's name.
${TEST}	|测试用例名称
${USERAGENT}	|包含 ${BROWSER}, ${BROWSER_VERSION}, ${OS}, and ${OS_VERSION} (separated by underscores).
${BROWSER}	|浏览器名称
${BROWSER_VERSION}	|浏览器版本
${OS}	|操作系统名称
${OS_VERSION}	|操作系统版本
${TEST_ID}|	Resolves to test-${TEST_INDEX} if TestCafe can associate this screenshot or video with a specific test; resolves to an empty string otherwise (for instance, when a single video is recorded for the entire test run).
${RUN_ID}|	Resolves to run-${QUARANTINE_ATTEMPT} for screenshots taken when quarantine mode is enabled; resolves to an empty string for videos and for screenshots taken when quarantine mode is disabled.

# 录屏
**注意：**录屏只允许在谷歌浏览器，火狐浏览器，edge浏览器，当你使用远程浏览器测试时无法录屏

**安装软件** <a href="https://ffmpeg.org/">FFmpeg library</a>

## use
1.命令行

testcafe chrome ./ **--video artifacts/videos**

2.runner.screenshots
```
runner.video('artifacts/videos');
```
3.配置文件
```
{
  "videoPath":"artifacts/videos"
}
```

## 录屏选项
Option|	Type|		Description|		Default Value
:--:|:--:|	:--:|:--:
failedOnly	|	Boolean	|	默认为false,当为true时只记录失败的用例。|		false
singleFile|		Boolean|		默认为false,当为true时所有录屏在同一个MP4文件|		false
ffmpegPath	|	String	|	The path to the FFmpeg codec executable.	|	Auto-detected
pathPattern	|	String|		A pattern that defines how TestCafe composes the relative path to a video file.|	 See Screenshot and Video Directories.	See Default Path Pattern.


# 拦截http请求
## 记录http请求


[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
