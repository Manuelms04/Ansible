# ANSIBLE

![ansible](/ansible1.png)

# **Estudio del Módulo `apt` en Ansible**  

## **1.- Nombre del módulo: `apt`**  

### **Descripción**  
El módulo `apt` de Ansible se utiliza para gestionar paquetes en sistemas basados en Debian y Ubuntu. Permite instalar, actualizar, eliminar y administrar paquetes utilizando el gestor de paquetes `apt`. Es muy útil para la automatización de la gestión de software en servidores.

---

## **2.- Ejemplos de funcionamiento**  

### **Ejemplo 1: Instalar un paquete**  
En este playbook instalaremos el servidor web `nginx` en un sistema Ubuntu/Debian.

#### **Archivo:** `instalar_nginx.yaml`
```yaml
- name: Instalar Nginx en un servidor Debian/Ubuntu
  hosts: all  # Reemplazar con el nombre del host o grupo de hosts
  become: true  # Permite ejecutar el playbook con permisos de superusuario  
  tasks:
    - name: Instalar el paquete Nginx
      ansible.builtin.apt:
        name: nginx
        state: present
```
#### **Comando para ejecutar el Playbook**
```bash
ansible-playbook instalar_nginx.yaml
```

#### **Verificación (En el cliente)**  
```bash
systemctl status nginx
```
Si `nginx` está en ejecución, la instalación fue exitosa.

![Captura de instalación](/img/instalar_nginx.png)

---

### **Ejemplo 2: Actualizar todos los paquetes del sistema**  
Este playbook actualizará todos los paquetes instalados en el sistema a sus últimas versiones.

#### **Archivo:** `actualizar_sistema.yaml`
```yaml
- name: Actualizar los paquetes del sistema
  hosts: all  # Reemplazar con el nombre del host o grupo de hosts
  become: true  # Permite ejecutar el playbook con permisos de superusuario  
  tasks:
    - name: Actualizar la lista de paquetes
      ansible.builtin.apt:
        update_cache: yes

    - name: Actualizar todos los paquetes
      ansible.builtin.apt:
        upgrade: dist
```
#### **Comando para ejecutar el Playbook**
```bash
ansible-playbook actualizar_sistema.yaml
```

#### **Verificación (En el cliente)**  
```bash
apt list --upgradable
```
Si no hay paquetes listados, significa que el sistema está actualizado.

![Captura de actualización](/img/actualizar_sistema.png)

---

### **Ejemplo 3: Eliminar un paquete**  
En este playbook eliminaremos el paquete `apache2` si está instalado.

#### **Archivo:** `eliminar_apache.yaml`
```yaml
- name: Eliminar Apache2 del sistema
  hosts: all  # Reemplazar con el nombre del host o grupo de hosts
  become: true  # Permite ejecutar el playbook con permisos de superusuario  
  tasks:
    - name: Eliminar el paquete Apache2
      ansible.builtin.apt:
        name: apache2
        state: absent
```
#### **Comando para ejecutar el Playbook**
```bash
ansible-playbook eliminar_apache.yaml
```

#### **Verificación (En el cliente)**  
```bash
dpkg -l | grep apache2
```
Si no hay salida, significa que `apache2` ha sido eliminado correctamente.

![Captura de eliminación](/img/eliminar_apache.png)

---

## **3.- Referencias**  
- [Documentación oficial de Ansible sobre el módulo `apt`](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/apt_module.html)  
- [Guía oficial de Ansible](https://docs.ansible.com/ansible/latest/user_guide/index.html)  
- [Manuel Domínguez](https://github.com/mftienda)
---
