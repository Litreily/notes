# Network Interface

根据网卡名称获取网卡接口信息

```py
import winreg as wr

IF_REG = r'SYSTEM\CurrentControlSet\Control\Network\{4d36e972-e325-11ce-bfc1-08002be10318}'
def getInterfaceByName(name):
    '''Get guid of interface from regedit of windows system
    Args:
        name: interface name

    Returns:
        An valid guid value or None.

    Example:
        getInterfaceByName('Company')
    '''
    reg = wr.ConnectRegistry(None, wr.HKEY_LOCAL_MACHINE)
    reg_key = wr.OpenKey(reg, IF_REG)
    for i in range(wr.QueryInfoKey(reg_key)[0]):
        subkey_name = wr.EnumKey(reg_key, i) 
        try:
            reg_subkey = wr.OpenKey(reg_key, subkey_name + r'\Connection')
            Name = wr.QueryValueEx(reg_subkey, 'Name')[0]
            wr.CloseKey(reg_subkey)
            if Name == name:
                return r'\Device\NPF_' + subkey_name
        except FileNotFoundError:
            pass
    return None

print(getInterfaceByName(u'以太网 3'))
```

```bash
$ python winreg_test.py
\Device\NPF_{80862F2B-A799-4E4F-9D78-ABD134934554}
```
