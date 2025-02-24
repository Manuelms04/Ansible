# Ansible

![ansible](/img/ansible1.png)

# **Estudio del Módulo `apt` en Ansible**  

## **1.- Nombre del módulo: `apt`**  

### **Descripción**  
El módulo `apt` de Ansible se utiliza para gestionar paquetes en sistemas basados en Debian y Ubuntu. Permite instalar, actualizar, eliminar y administrar paquetes utilizando el gestor de paquetes `apt`. Es muy útil para la automatización de la gestión de software en servidores.

---

## **2.- Ejemplos de funcionamiento**  

### **Ejemplo 1: Instalar un paquete**  
En este playbook instalaremos el servidor web `nginx` en un sistema Ubuntu/Debian.

#### **Archivo:** `instalar_nginx.yml`
```yaml
- name: Instalar Nginx en un servidor Debian/Ubuntu
  hosts: servidores  # Reemplazar con el nombre del host o grupo de hosts
  become: true  # Permite ejecutar el playbook con permisos de superusuario
  tasks:
    - name: Instalar el paquete Nginx
      ansible.builtin.apt:
        name: nginx
        state: present
```
#### **Comando para ejecutar el Playbook**
```bash
ansible-playbook instalar_nginx.yml
```

#### **Verificación**  
```bash
systemctl status nginx
```
Si `nginx` está en ejecución, la instalación fue exitosa.

---

### **Ejemplo 2: Actualizar todos los paquetes del sistema**  
Este playbook actualizará todos los paquetes instalados en el sistema a sus últimas versiones.

#### **Archivo:** `actualizar_sistema.yml`
```yaml
- name: Actualizar los paquetes del sistema
  hosts: servidores
  become: true
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
ansible-playbook actualizar_sistema.yml
```

#### **Verificación**  
```bash
apt list --upgradable
```
Si no hay paquetes listados, significa que el sistema está actualizado.

---

### **Ejemplo 3: Eliminar un paquete**  
En este playbook eliminaremos el paquete `apache2` si está instalado.

#### **Archivo:** `eliminar_apache.yml`
```yaml
- name: Eliminar Apache2 del sistema
  hosts: servidores
  become: true
  tasks:
    - name: Eliminar el paquete Apache2
      ansible.builtin.apt:
        name: apache2
        state: absent
```
#### **Comando para ejecutar el Playbook**
```bash
ansible-playbook eliminar_apache.yml
```

#### **Verificación**  
```bash
dpkg -l | grep apache2
```
Si no hay salida, significa que `apache2` ha sido eliminado correctamente.

---

## **3.- Referencias**  
- [Documentación oficial de Ansible sobre el módulo `apt`](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/apt_module.html)  
- [Guía oficial de Ansible](https://docs.ansible.com/ansible/latest/user_guide/index.html)  

---

✅ **Recuerda:** Toma capturas de pantalla mientras ejecutas los Playbooks y agrégalas a tu repositorio. ¡Listo para subir a GitHub! 🚀
