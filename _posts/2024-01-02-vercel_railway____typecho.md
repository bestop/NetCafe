---
title: Vercel+Railway免费部署Typecho

---

通常搭建一个动态博客都要有自己的服务器，今天介绍一下如何利用Vercel+Railway免费部署动态博客Typecho。<br><br>
1. 利用[Railway](https://railway.app/)建立数据库<br>
在Railway中新建项目，类型选择Provision MySQL，建好后在变量中获取相关数据库信息备用。<br><br>
2. 配置Typecho<br>
在[Typecho 官网](https://typecho.org/)下载正式版安装文件，解压到本地文件。<br>
a. 编辑 install.php文件，注释掉第773行至775行；<br>

```
#    if (!$writeable) {//第773行
#        $errors[] = _t('上传目录无法写入, 请手动将安装目录下的 %s 目录的权限设置为可写然后继续升级', $uploadDir);
#    }//第775行
```
b. 根目录添加 vercel.json文件；<br>
```
{
  "functions": {
    "api/index.php": {
      "runtime": "vercel-php@0.6.0"
    }
  },
  "routes": [{ "src": "/(.*)", "dest": "/api/index.php" }]
}
```
注意：runtime 这里vercel-php如使用旧版本会因为与 Vercel 网站上设置的 Node.js 版本不兼容导致部署时报错，需更新至适配版本。<br>
c. 根目录创建 api 目录并在目录下添加 index.php文件；<br>
```
<?php
$file= __DIR__ . '/..'.$_SERVER["PHP_SELF"];

if(file_exists($file))
{
   return false;
}
else
{
    require_once __DIR__ . '/../index.php';
}
#echo $_SERVER["PHP_SELF"];
```
<br>
d. 根目录添加 config.inc.php文件。<br>
```
<?php
/**
 * Typecho Blog Platform
 *
 * @copyright  Copyright (c) 2008 Typecho team (http://www.typecho.org)
 * @license    GNU General Public License 2.0
 * @version    $Id$
 */

/** 开启https */
define('__TYPECHO_SECURE__',true);

/** 定义根目录 */
define('__TYPECHO_ROOT_DIR__', dirname(__FILE__));

/** 定义插件目录(相对路径) */
define('__TYPECHO_PLUGIN_DIR__', '/usr/plugins');

/** 定义模板目录(相对路径) */
define('__TYPECHO_THEME_DIR__', '/usr/themes');

/** 后台路径(相对路径) */
define('__TYPECHO_ADMIN_DIR__', '/admin/');

/** 设置包含路径 */
@set_include_path(get_include_path() . PATH_SEPARATOR .
__TYPECHO_ROOT_DIR__ . '/var' . PATH_SEPARATOR .
__TYPECHO_ROOT_DIR__ . __TYPECHO_PLUGIN_DIR__);

/** 载入API支持 */
require_once 'Typecho/Common.php';

/** 程序初始化 */
Typecho_Common::init();

/** 定义数据库参数 */
$db = new Typecho_Db('Pdo_Mysql', 'typecho_');
$db->addServer(array (
  'host' => '数据库地址',
  'user' => '数据库用户名',
  'password' => '数据库密码',
  'charset' => 'utf8mb4',
  'port' => '数据库端口号',
  'database' => '数据库名称',
  'engine' => 'MyISAM',
), Typecho_Db::READ | Typecho_Db::WRITE);
Typecho_Db::set($db);
```
根据第一步中得到的Railway 数据库信息更新对应的数据库参数。<br>
3. 利用 [Vercel ](https://vercel.com/)部署<br>
a. 本地电脑安装并配置 vscode、node.js 和 npm，项目文件下通过 npm 安装 Vercel CLI，<br>
`npm -g install vercel`
<br>
b. CLI登录Vercel，<br>
`vc login`
<br>
c. 登录成功后部署，<br>
`vc`
<br>
一路回车，<br>
```
Vercel CLI 28.10.1
? Set up and deploy “部署路径”? [Y/n] y （直接回车）
? Which scope do you want to deploy to? 用户名（直接回车）
? Link to existing project? [y/N] n（直接回车）
? What’s your project’s name? 项目名称（直接回车）
? In which directory is your code located? ./（直接回车）
Local settings detected in vercel.json:
No framework detected. Default Project Settings:
- Build Command: `npm run vercel-build` or `npm run build`
- Development Command: None
- Install Command: `yarn install`, `pnpm install`, or `npm install`
- Output Directory: `public` if it exists, or `.`
? Want to modify these settings? [y/N] n （直接回车）
🔗  Linked to 用户名/项目名称 (created .vercel and added it to .gitignore)
🔍  Inspect: https://vercel.com/用户名/项目名称/部署事件唯一码 [3s]
✅  Production: Vercel 自动分配的以 vercel.app 结尾的网址 [24s]
📝  Deployed to production. Run `vercel --prod` to overwrite later (https://vercel.link/2F).
💡  To change the domain or build command, go to https://vercel.com/用户名/项目名称/settings
```
如果出现 Production 即可，如显示 Preview 时候需要运行，<br>
`vc --prod`
<br>
重点：由于 *.vercel.app 在国内无法访问，需在vercel内绑定域名。<br>
CNAME  cname-china.vercel-dns.com<br>
4. 安装 Typecho<br>
地址栏输入域名 /install.php进入Typecho安装界面。



