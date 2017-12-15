# Полезные приложения

## [Sublime Text](http://www.sublimetext.com/) - кроссплатформенный редактор кода.

_Рекомендую установить **portable** версию для пользователей Windows._

* [Установка Package Control.](https://sublime.wbond.net/installation)<br>
  Самый простой способ установки - это прямо в консоли Sublime Text. Консоль доступна с помощью `` ctrl+` `` или<br>
  `View > Show Console menu`. После открытия вставьте соответствующий Python код для Вашей версии Sublime Text в консоль.

Для Sublime Text 3:

```python
import urllib.request,os,hashlib; h = '2deb499853c4371624f5a07e27c334aa' + 'bf8c4e67d14fb0525ba4f89698a6d7e1'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
```

Для Sublime Text 2:

```python
import urllib2,os,hashlib; h = '2deb499853c4371624f5a07e27c334aa' + 'bf8c4e67d14fb0525ba4f89698a6d7e1'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); os.makedirs( ipp ) if not os.path.exists(ipp) else None; urllib2.install_opener( urllib2.build_opener( urllib2.ProxyHandler()) ); by = urllib2.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); open( os.path.join( ipp, pf), 'wb' ).write(by) if dh == h else None; print('Error validating download (got %s instead of %s), please try manual install' % (dh, h) if dh != h else 'Please restart Sublime Text to finish installation')
```

* Установка пакетов доступна с помощью `Preferences > Package Control`, в списке выбрать `Install Package`. Через несколько секунд появится список доступных пакетов.

## [Fenix Web Server](https://github.com/coreybutler/fenix)

![Fenix Web Server](https://github.com/coreybutler/fenix/blob/gh-pages/img/osx/banner_device.png?raw=true)

## [Open Server](http://open-server.ru/) - сервер под windows

![Open Server](http://open-server.ru/files/l2.png)
