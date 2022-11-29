# Icloud 888

## 缘起

2021年11月份，中国大陆地区icloud域名由`icloud.com`迁移至`icloud.com.cn`。python package `pyicloud`没有做针对性修改，这就造成了以pyicloud包为依赖的home-assistant `icloud集成`无法正常使用。

通过将 pyicloud / base.py 中的domain由icloud.com改为icloud.com.cn，可解决这一问题。但大多数人使用docker容器部署home-assistant，这使得该改动无法持久化，升级home-assistant或重启容器均会导致改动失效。

故此，就搞了这么个HA自定义集成：把原有icloud集成与pyicloud打包起来，将pyicloud中的icloud访问域名修改为icloud.com.cn，并相应修改了icloud集成的依赖。由于/config目录是持久化的，所以在其中的自定义集成不会随着升级、容器重启而发生改变，这样问题就解决啦。

## 使用方法

首先将本集成拷贝至homeassistant `/config/custom_components`目录下，推荐方法如下：

```bash
cd /config/custom_components
git clone https://github.com/louisslee/icloud888.git

```

clone完成后，重启HA即可在配置-》设备与服务-》添加集成中找到icloud888集成，添加与使用方法同原icloud集成一样，这里就不多介绍了。

__需要注意的是, 由于icloud888与原icloud集成相比，除了domain以外，其他完全一致，甚至包括unique_id等等，建议不要与原icloud集成配置同一个icloud账号。__
