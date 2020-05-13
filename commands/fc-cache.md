# fc-cache

``` bash
sudo mkdir /usr/share/fonts/custom
sudo cp /path/to/fontfile  /usr/share/fonts/custom
sudo chmod 644 /usr/share/fonts/custom/*

cd /usr/share/fonts/custom
sudo mkfontscale
sudo mkfontdir
sudo fc-cache -fv
```

