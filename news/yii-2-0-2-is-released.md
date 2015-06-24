> [ԭ�ģ�www.yiiframework.com/news/](http://www.yiiframework.com/news/84/yii-2-0-2-is-released/)  
�����룺@qiansen1386 (������˼��) У�ԣ�Ҳ�����~ ʱ�䣺2015��1��11�� ת�����ߣ�[PANDOC ONLINE](https://foliovision.com/seo-tools/pandoc-online)

> �ر����ѣ����� Yii �ĵ�֮����ⲿ���Ӿ������Ϊԭ�����ӣ���δ�ṩ�������ӡ�������Ҫ�����Լ����Ҵ��������ȫ����Ļ���־Ը���ṩ�ĺ����汾�������ر���Ҫ��Ҳ���Ը�����[�ύ�������󣬲�������Ǳ���� Markdown ��ʽ���ļ�](https://github.com/yii2-chinesization/yii2-zh-cn/issues)��

Yii 2.0.2 �����ˣ�
=====================

�����ҵ�����������Yii ��� 2.0.2 �汾¡�������ˡ�Ҫ��װ���������ð汾�������ǣ���ǰ�� [http://www.yiiframework.com/download/](http://www.yiiframework.com/download/) �˽������Ѷ��

2.0.2 �汾��һ�� Yii 2 ���޶����������� 40 ��С�Ĺ��ܸĽ��� bug �޸����������޸��б���μ� [change log](https://github.com/yiisoft/yii2/blob/2.0.2/framework/CHANGELOG.md)���ش˸�л[���еĹ�����](https://github.com/yiisoft/yii2/graphs/contributors)����л����Ϊ Yii �ĸĽ������������ѵı���ʱ�䣬����Ϊ�����ǵ�֧�ֲ����˴˴εķ�����

�����ͨ���Ǳ꣨star�����ע��watch��[Yii 2.0 GitHub ��Ŀ](https://github.com/yiisoft/yii2)�����˽⿪�����ȡ�Ҳ���Թ�ע Yii �� [����](https://twitter.com/yiiframework)��[����С��](https://www.facebook.com/groups/yiitalk/) �뿪��С�鱣�ֻ�����

���棬���ǽ��оٴ˴θ����е�һЩ�ص㡣

·�ɱ�����Route Alias��
-----------

֮ǰ�����Ŀ�ܴ���ֻ֧�ִ����ļ�·���� URL �ı��������ڣ���������˶�·�ɱ�����֧�֡�������ԣ�����Ը�·�����ñ�����Ȼ������Ҫ������Ӧ�� URL ��ʱ�򣬾Ϳ����ñ���ָ���·�ɡ�·�ɱ���ע��ͨ�� `Url::to()` �Լ� `Url::toRoute()`���ַ���ʵ�֡��������ԣ�

```php
use yii\helpers\Url;
     
Yii::setAlias('@posts', 'post/index');
 
// /index.php?r=post/index
echo Url::to(['@posts']);
echo Url::toRoute('@posts');
```

��ᷢ�֣���·�ɱ����Ϊ�ǹ̶�ֵ�����㲻��ÿ��·�ɸı��ʱ�򣬶��޸ĸ�·�ɵ����� URL ���ɴ��롣��ʱ��·�ɱ����ͻ�ǳ�֮���á�
You may find route alias to be useful when your route design is not fixed and you want to avoid changing your URL creation code everywhere when your route design is changed.

����������� Dependent Component Configuration
---------------------------------

����������������Ҫ������Ϊĳһ������Ӧ������� ID �����ԣ����磺`yii\caching\DbCache::db`��`yii\web\CacheSession::cache`�����ƣ�Ϊ�˱��������µ�Ӧ���������ڱ��ڵ�Ԫ���Ե�Ŀ�ģ��������Ҫֱ����һ�������ڴ���������������������飬�����ø����ԡ����ڣ��������������

Many components contain properties that should be configured to be the ID of a dependent application component, such as `yii\caching\DbCache::db`, `yii\web\CacheSession::cache`. Sometimes, to avoid introducing new application component or for unit testing purpose, you may want to directly configure such a property with a configuration array that can be used to create the dependent component. You can do so now like the following:

```php
$cache = Yii::createObject([
    'class' => 'yii\caching\DbCache',
    'db' => [
        'class' => 'yii\db\Connection',
        'dsn' => '...',
    ],
]);
```
������ڿ���һ���������ⲿ��������࣬����������·������׵ػ������Ч����

If you are developing a new class that depends on an external component, you may use the following approach to obtain the similar support readily:

```php
use yii\base\Object;
use yii\db\Connection;
use yii\di\Instance;
 
class MyClass extends Object 
{
    public $db = 'db';
 
    public function init() 
    {
        $this->db = Instance::ensure($this->db, Connection::className());
    }
}
```

���ϴ����У�`db` ���Կɱ�����Ϊ�������ָ�ʽ�ĳ�ʼֵ�е�����һ�֣�

-   ָ��ĳӦ����� ID ���ַ�����
-   ĳ `yii\db\Connection` ʵ����
-   ���������� `yii\db\Connection` ʵ�����������顣

���õ�������ַ��Immutable Slug��
--------------

> ����ע�� Slug ����ͨ�����µ� ID ����������ֵ�Զ����ɵ��� `-` �ָ��� URL��[wordpress ������һ������Ľ���](http://codex.wordpress.org/zh-cn:%E9%A1%B5%E9%9D%A2#.E4.BF.AE.E6.94.B9.E9.A1.B5.E9.9D.A2.E7.9A.84URL.EF.BC.88.E6.88.96.22Slug.22.EF.BC.89)�����¼�� slug��

��������ʹ�� `yii\behaviors\SluggableBehavior`�������ڿ���Ӧ��һ����Ϊ `immutable` �������ԡ�ͨ����������Ϊ true������ȷ��һ�� slug �Ѿ����ɹ��ˣ���ô��ʹ�Ƕ�Ӧ��Դ����ֵ���޸Ĺ�����Ҳ�����ٸ����ˡ���� SEO ���Ż��ر����ã���Ϊ�㲻����Ҫ�޸�һ���Ѿ������� slug URL �ġ�����ע���Ѿ�����¼�������޸� URL ���򽵵�Ȩ�أ�����ֱ��ɾ������ѧ�о������������޸� URL �ǻ�����վ����Ȩ�ص���Ҫ�ֶ�֮һ��

����ѡ���������Ի��ˣ�DatePicker Language Fallback��
----------------------------

`yii\jui\DatePicker` С��������֧�����Ի��ˡ���Ҫ�ڵ����� `language` ���Ա�����Ϊ�����е�����ʶ������Ϊ��ε�������ʱ��������á�˵�������ǣ����� `language` ������Ϊ `de-DE`������-�µ�����, �Ҹ�С�����޷��ҵ���Ϊ `/ui/i18n/datepicker-de-DE.js` �������ļ������ͻ���˵����� `de` Ҳ���ǵ��������Ѱ�� `/ui/i18n/datepicker-de.js` �����ļ���

������֤����Passing Validation Errors��
-------------------------

`yii\base\Model` ����������һ������ķ����� `addErrors()`���������������֤���󣬴�һ��ģ���ഫ�ݵ���һ�����������ԣ�����������һ����ģ���ࣨForm Model�����ñ�ģ�Ͱ�����һ�����¼ģ�ͣ�ActiveRecord Model��������ܻ���Ҫ�ѱ�ģ�͵���֤���󴫵ݵ����¼֮�У���ʱ��Ϳ������ɵص��ø÷�����ʵ�֣�

```php
use yii\base\Model;
use yii\db\ActiveRecord;
 
class MyForm extends Model 
{
    public $model;
 
    public function process()
    {
        // ...
        if (!$this->validate()) {
            $this->model->addErrors($this->getErrors());
            // ....
        }
    }
}
```
                    