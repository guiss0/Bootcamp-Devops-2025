
sed -i 's/IT777/IT771/g' "archivo.conf"

sed -i 's/{IP A CAMBIAR}/{IP NUEVA ASIGNADA}/g' "archivo.conf"

sed -i 's/{OLD MAC ADDRESS}}/{NUEVA MAC ADDRESS}}/g' "archivo.conf"

```bash
#!/bin/bash


#Colors

color='\033[0;32m' 
NC='\033[0m'
Red='\033[0;31m' 
Cyan='\033[0;36m' 

# Reset
Color_Off='\033[0m'       # Text Reset

# Regular Colors
Black='\033[0;30m'        # Black
Red='\033[0;31m'          # Red
#Green='\033[0;32m'        # Green
Yellow='\033[0;33m'       # Yellow
Blue='\033[0;34m'         # Blue
Purple='\033[0;35m'       # Purple
White='\033[0;37m'        # White
Magenta='\033[0;95m'       # Magenta



function rHost (){
echo -e "Para cambiar el nombre del host, escribe que host quieres cambiar y luego selecciona el nombre del nuevo host"
echo -e "Ejemplo; host que quiero cambiar; IT777, host nuevo que quiero asignarle IT007"

echo -e "Escribe aqui el nombre del host a cambiar: "
read oldHost

echo -e "Escribe aqui el nombre del nuevo host"
read newHost
sed -i "s/"$oldHost"/"$newHost"/g" "archivo.conf"

echo -e "[!] Nombre del host cambiado!"
echo -e "[!] Presiona enter para continuar..."
read enter1
}


function rMac (){
echo -e "Para cambiar la Mac address, escribe la mac que quieres cambiar y luego escribe la nueva mac address"
echo -e "Ejemplo; Si la mac address que quiero cambiar es 00-00-77-32-66-F1, y la nueva mac address 77-77-77-D3-D2-D1"

echo -e "Escribe aqui la mac address a cambiar: "
read oldMac

echo -e "Escribe aqui la nueva mac address"
read newMac

sed -i "s/"$oldMac"/"$newMac"/g" "archivo.conf"

echo -e "[!] Mac address cambiada!"
echo -e "[!] Presiona enter para continuar..."
read enter2
}


function rIp (){
echo -e "Selecciona la ip a cambiar y escribe la nueva ip asignada a sustituir por la vieja direccion ip"

echo -e "Escribe aqui la IP a cambiar: "
read oldIp

echo -e "Escribe aqui la nueva IP"
read newIp 

sed -i "s/"$oldIp"/"$newIp"/g" "archivo.conf"

echo -e "[!] Ip cambiada!"
echo -e "[!] Presiona enter para continuar..."
read enter3
}



function rArea (){
echo -e "Selecciona el Area a cambiar y escribe la nueva Area a sustituir"
echo -e "Recuerda que las areas son catalogadas asi; #Area\n"
echo -e "Escribe aqui El area a cambiar: "
read oldArea

echo -e "Escribe aqui la nueva Area"
read newArea

sed -i -e "s/"$oldArea"/"$newArea"/g" "archivo.conf"

echo -e "[!] Area cambiada!"
echo -e "[!] Presiona enter para continuar..."
read enter3
}



function menu () {
while true; do
clear
  echo "SELECCIONA LO QUE QUIERES CAMBIAR" 
  echo  "~~~~~~~~~~~~~~~~~~~~~"
  echo -e "${Yellow}[!]${NC}${White} 1) HOST ${NC}"
  echo -e "${Yellow}[!]${NC}${White} 2) MAC ${NC}"
  echo -e "${Yellow}[!]${NC}${White} 3) IP ASIGNADA ${NC}"
  echo -e "${Yellow}[!]${NC}${White} 4) Area ${NC}"
 # echo -e "${Yellow}[!]${NC}${White} Presiona ${NC}"
 # echo -e "${Yellow}[!]${NC}${White} Presiona ${NC}"
  echo -e -n "${Red}[-]${NC}${White} Presiona q para salir${NC}\n\n\n\n"


  read -p "Ingresa tu eleccion (1, 2, 3, 4, 5 o 6): " choice

  case $choice in
    1) rHost;;
    2) rMac;;
    3) rIp;;
    4) rArea;;
    q) exit;;
    *) echo -e "[-] Eleccion invalida. Por favor, intenta nuevamente.";;
  esac
done

}

menu
```

