> [ԭ�ģ�www.yiiframework.com/news/](http://www.yiiframework.com/news/82/yii-2-0-1-is-released/)  
�����룺@qiansen1386 (������˼��) У�ԣ�Ҳ�����~ ʱ�䣺2014��12��7�� ת�����ߣ�[PANDOC ONLINE](https://foliovision.com/seo-tools/pandoc-online)

> �ر����ѣ����� Yii �ĵ�֮����ⲿ���Ӿ������Ϊԭ�����ӣ���δ�ṩ�������ӡ�������Ҫ�����Լ����Ҵ��������ȫ����Ļ���־Ը���ṩ�ĺ����汾�������ر���Ҫ��Ҳ���Ը�����[�ύ�������󣬲�������Ǳ���� Markdown ��ʽ���ļ�](https://github.com/yii2-chinesization/yii2-zh-cn/issues)��

Yii 2.0.2 �����ˣ�
=====================

�����ҵ�����������Yii ��� 2.0.1 �汾¡�������ˡ�Ҫ��װ���������ð汾�������ǣ���ǰ�� [http://www.yiiframework.com/download/](http://www.yiiframework.com/download/) �˽������Ѷ��

2.0.1 �汾��һ�� Yii 2.0 ���޶����������� 90 ��С�Ĺ��ܸĽ��� bug �޸����������޸��б���μ� [change log](https://github.com/yiisoft/yii2/blob/2.0.2/framework/CHANGELOG.md)���ش˸�л[���еĹ�����](https://github.com/yiisoft/yii2/graphs/contributors)����л����Ϊ Yii �ĸĽ������������ѵı���ʱ�䣬����Ϊ�����ǵ�֧�ֲ����˴˴εķ�����

�����ͨ���Ǳ꣨star�����ע��watch��[Yii 2.0 GitHub ��Ŀ](https://github.com/yiisoft/yii2)�����˽⿪�����ȡ�Ҳ���Թ�ע Yii �� [����](https://twitter.com/yiiframework)��[����С��](https://www.facebook.com/groups/yiitalk/) �뿪��С�鱣�ֻ�����

���棬���ǽ��оٴ˴θ����е�һЩ�ص㡣

ǿ�� Asset ת����Forcing Asset Conversion��
------------------------

Asset bundle ֧���Զ����� asset ת��������Ҫ�� LESS ת��Ϊ CSS��Ȼ�����ò���Ҫ���Ѻܴ�Ĵ��ۣ���ȷ�������õض� Asset Դ�ļ��ĸĶ����м�⣬�����ǵ�����ǰ����Դ�У���������������ǰ����Դʱ��Ϊ�˽��������⣬�����ڿ����������� `assetManager`���Ӷ�ʼ��ǿ��ִ��ǰ����Դת������ע��Ҳ���ǲ�����ˣ���

```php
[
    'components' =>  [
        'assetManager' => [
            'converter' => [
                'forceConvert' => true,
            ]
        ]
    ]
];
```

ѡ���Ӳ�ѯ��Selecting Sub-queries��
---------------------

Query builder ֧���ڲ�ͬ�ĵط�ʹ���Ӳ�ѯ��������Ҳ������ `SELECT` �����е����Ӳ�ѯ���������ԣ�

```php
$subQuery = (new Query)->select('COUNT(*)')->from('user');
$query = (new Query)->select(['id', 'count' => $subQuery])->from('post');
// $query represents the following SQL:
// SELECT `id`, (SELECT COUNT(*) FROM `user`) AS `count` FROM `post`
```

��ֹ�� AJAX ���ظ����� CSS
--------------------------------

֮ǰ��Yii �Ѿ��ṩ�˶��ڷ�ֹ�� AJAX ��Ӧ���ظ�������ͬ JavaScript �ļ���֧�֡�������Ҳ�ṩ�˶Է�ֹ�� AJAX ��Ӧ���ظ�������ͬ CSS �ļ���֧�֡�Ҫʹ�øù��ܣ���ֻ���������򵥵ص��� `YiiAsset` asset bundle��

```php
yii\web\YiiAsset::register($view);
```

��� schema ���棨Flushing Schema Cache��
---------------------

������һ���µĿ���̨������������ schema ���档��������Ҫ������Ҫ�������ݿ� schema �����������������Ĵ���ʱ�����á�ֱ�������������
A new console command is added to allow you to flush schema cache. This is useful when you deploy code that cause DB schema changes to production servers. Simply run the command as follows:

```cmd
yii cache/flush-schema
```

��������ǿ(Helpers��
-----------------------

`Html::cssFile()` ��������֧�� `noscript` ѡ���ˣ���������ɵ� `link` ��ǩ��װ�� `noscript` ��ǩ����Ҳ����ͨ������ asset bundle �� `AssetBundle::cssOptions` ���ԣ������ø�ѡ����磺

```php
use yii\helpers\Html;
 
echo Html::cssFile('/css/jquery.fileupload-noscript.css', ['noscript' => true]);
```

֮ǰ `StringHelper::truncate()` ֻ֧�ִ����ı���ʽ���ַ�����������Ҳ֧�� HTML ��ʽ���ַ�����������ȷ�����̺�ķ���ֵ����Ϊ��Ч�� HTML �ַ�����

`Inflector` ��������һ�������� `sentence()`�������һС�鵥�ʴ����ɾ��ӡ�����˵��

```php
use yii\helpers\Inflector;
 
$words = ['Spain', 'France'];
echo Inflector::sentence($words);
// �����Spain and France
 
$words = ['Spain', 'France', 'Italy'];
echo Inflector::sentence($words);
// �����Spain, France and Italy
 
$words = ['Spain', 'France', 'Italy'];
echo Inflector::sentence($words, ' & ');
// �����Spain, France & Italy
```

Bootstrap ��չ��ǿ
-----------------------------------

���ȣ�Twitter Bootstrap ������������ 3.3.x �İ汾���������Ҫ����ʹ��֮ǰ�İ汾�������������Ŀ�� `composer.json` ����ȷָ���ð汾��

һЩ Bootstrap С���������һЩ���ԡ���ο�[Class Reference](http://apidoc.yii2.cn/guide-widget-bootstrap.html)�˽���ࡣ

-   `yii\bootstrap\ButtonDropdown::$containerOptions`
-   `yii\bootstrap\Modal::$headerOptions`
-   `yii\bootstrap\Modal::$footerOptions`
-   `yii\bootstrap\Tabs::renderTabContent`
-   `yii\bootstrap\ButtonDropdown::$containerOptions`

MongoDB ��չ��ǿ
---------------------------------

���� `yii\mongodb\Query` �� `yii\mongodb\ActiveQuery`��֧�� `findAndModify` ����ѯ���޸ģ��������ٸ����ӣ�

```php
User::find()->where(['status' => 'new'])->modify(['$set'=>['status' => 'processing']]);
```

Ϊ����ʾ MongoDB �Ĳ�ѯ���̣��������һ���µ� debug ��塣Ҫ���ø���壬ֻ������������� Yii debugger��

```php
[
    'class' => 'yii\debug\Module',
    'panels' => [
        'mongodb' => [
            'class' => 'yii\mongodb\debug\MongoDbPanel',
        ]
    ],
]
```

Redis ��չ��ǿ
-------------------------------

Yii Redis ��չ��֧��ʹ�� UNIX socket ���ӣ�������ڻ��� TCP �����ӷ�ʽ���� 50%��Ҫʹ������ֻ���������� redis ���Ӽ��ɣ�

```php
[
    'class' => 'yii\redis\Connection',
    'unixSocket' => '/var/run/redis/redis.sock',
]
```