# ANSIBLE

![ansible](/ansible1.png)

# **Estudio del Módulo `hostname` en Ansible**  

## **1.- Nombre del módulo: `hostname`**  

### **Descripción**  

El módulo `hostname` de Ansible permite gestionar el nombre del host de un sistema. Se utiliza para cambiar el nombre del host o verificar el nombre actual. Este módulo es útil cuando necesitas automatizar la configuración de nombres de máquina a través de tus servidores, asegurando consistencia en el entorno.

---

## **2.- Ejemplos de funcionamiento**  

### **Ejemplo 1: Cambiar el nombre del host**  
- Este playbook cambia el nombre del host de a `servidor1` en un sistema Ubuntu/Debian.

#### **Archivo:** `cambiar_hostname.yaml`
```yaml
- name: Cambiar el nombre del host a servidor1
  hosts: all  # Reemplazar con el nombre del host o grupo de hosts
  become: true  # Permite ejecutar el playbook con permisos de superusuario  
  tasks:
    - name: Establecer el nombre del host
      ansible.builtin.hostname:
        name: servidor1
```
#### **Comando para ejecutar el Playbook**
```bash
ansible-playbook cambiar_hostname.yaml
```

#### **Verificación (En el cliente)**  
```bash
hostname
```
El comando debería devolver `servidor1`.
--- 

🚨 **Ejecucion:** 🚨

![ejecucion1](/img/ejecucion1.png)
---

🚨 **COMPROBACION:** 🚨

![comprobacion1](/img/comprobacion1.png)

---

### **Ejemplo 2: Verificar el nombre del host**  
- Este playbook obtiene el nombre del host actual del sistema sin realizar ningún cambio.

#### **Archivo:** `verificar_hostname.yaml`
```yaml
- name: Verificar el nombre del host
  hosts: all  # Reemplazar con el nombre del host o grupo de hosts
  tasks:
    - name: Obtener el nombre del host
      ansible.builtin.hostname:
        name: "{{ ansible_hostname }}"
      register: result

    - name: Mostrar el nombre del host
      debug:
        msg: "El nombre del host es: {{ result }}"
```
#### **Comando para ejecutar el Playbook**
```bash
ansible-playbook verificar_hostname.yaml
```

#### **Verificación (En el cliente)**  
El playbook imprimirá el nombre actual del host.
--- 

🚨 **Ejecucion:** 🚨

![ejecucion2](/img/ejecucion2.png)
---

🚨 **COMPROBACION:** 🚨

![comprobacion2](/img/comprobacion2.png)

---

### **Ejemplo 3: Cambiar el nombre del host con el uso de una variable**  
- Este playbook cambia dinámicamente el nombre del host según una variable definida.

#### **Archivo:** `cambiar_hostname_variable.yaml`
```yaml
- name: Cambiar el nombre del host con una variable
  hosts: all  # Reemplazar con el nombre del host o grupo de hosts
  become: true  # Permite ejecutar el playbook con permisos de superusuario  
  vars:
    nuevo_hostname: servidor-dinamico
  tasks:
    - name: Cambiar el nombre del host
      ansible.builtin.hostname:
        name: "{{ nuevo_hostname }}"
```
#### **Comando para ejecutar el Playbook**
```bash
ansible-playbook cambiar_hostname_variable.yaml
```

#### **Verificación (En el cliente)**  
```bash
hostname
```
Debería devolver el nuevo nombre del host, `servidor-dinamico`.
--- 

🚨 **Ejecucion:** 🚨

![ejecucion3](/img/ejecucion3.png)
---

🚨 **COMPROBACION:** 🚨

![comprobacion3](/img/comprobacion3.png)

---

## **3.- Referencias**  
- [Documentación oficial de Ansible sobre el módulo `hostname`](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/hostname_module.html#ansible-collections-ansible-builtin-hostname-module)  
- [Guía oficial de Ansible](https://docs.ansible.com/ansible/latest/user_guide/index.html)  
- [Manuel Domínguez](https://github.com/mftienda)
---
