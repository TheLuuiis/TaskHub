# 📌 TaskHub - Gestor de Tareas Colaborativo  

TaskHub es una aplicación web para gestionar tareas personales y colaborativas.  
Permite a los usuarios crear, organizar y compartir tareas con grupos de trabajo de manera sencilla y eficiente..

---

## 🚀 Características principales  

- ✅ Registro e inicio de sesión de usuarios  
- 📝 Crear, editar, completar o eliminar tareas  
- 🔍 Filtros por estado (pendiente / completada) y prioridad  
- 👥 Creación de grupos de trabajo para compartir tareas  
- 📅 Organización por fecha límite  
- 📱 Interfaz moderna, limpia y responsive  

---

## 🛠️ Tecnologías utilizadas  

### Frontend  
- **HTML5** – estructura  
- **CSS3** – diseño y estilos responsive  
- **JavaScript** – validaciones, animaciones e interacción  

### Backend (ejemplo con Node.js)  
- **Node.js + Express** – servidor y API REST  
- **MySQL** – base de datos relacional  

> ⚡ También puede implementarse con **PHP + MySQL** en lugar de Node.js.  

---

## 📊 Estructura de la base de datos  

```sql
CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  email VARCHAR(150) UNIQUE NOT NULL,
  password VARCHAR(255) NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE tasks (
  id INT AUTO_INCREMENT PRIMARY KEY,
  user_id INT NOT NULL,
  title VARCHAR(150) NOT NULL,
  description TEXT,
  due_date DATE,
  priority ENUM('baja', 'media', 'alta') DEFAULT 'media',
  status ENUM('pendiente', 'completada') DEFAULT 'pendiente',
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (user_id) REFERENCES users(id)
);

CREATE TABLE groups (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(150) NOT NULL,
  created_by INT NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (created_by) REFERENCES users(id)
);

CREATE TABLE group_members (
  id INT AUTO_INCREMENT PRIMARY KEY,
  group_id INT NOT NULL,
  user_id INT NOT NULL,
  FOREIGN KEY (group_id) REFERENCES groups(id),
  FOREIGN KEY (user_id) REFERENCES users(id)
);

CREATE TABLE shared_tasks (
  id INT AUTO_INCREMENT PRIMARY KEY,
  task_id INT NOT NULL,
  group_id INT NOT NULL,
  FOREIGN KEY (task_id) REFERENCES tasks(id),
  FOREIGN KEY (group_id) REFERENCES groups(id)
);
