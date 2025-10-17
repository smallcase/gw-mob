- Open the Terminal application
- Type the following command and press Enter to open the sudo file in the nano editor, using your password when prompted: 
```shell
sudo nano /etc/pam.d/sudo
```
- Add the following line at the very beginning of the file:
```shell
auth sufficient pam_tid.so
```
