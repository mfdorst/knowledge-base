# Manage Wi-Fi with NetworkManager
Install NetworkManager
```
sudo pacman -S networkmanager
```
Enable NetworkManager
```
systemctl enable NetworkManager.service
systemctl start NetworkManager.service
```
List local networks
```
nmcli device wifi list
```
Connect to a network
```
nmcli device wifi connect <SSID> password <password>
```
Show existing connections
```
nmcli connection show
```
Activate an existing connection
```
nmcli connection up <SSID>
```
Delete a connection
```
nmcli connection delete <SSID>
```
See a list of network devices and their state
```
nmcli device
```
Turn Wi-Fi off
```
nmcli radio wifi off
```
