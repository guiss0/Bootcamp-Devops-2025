 cat archivo.conf | grep host | awk {'print $2,$7'} | tr -d ';}'
