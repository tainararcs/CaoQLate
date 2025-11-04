# Cão Q-Late – Sistema de Agendamento para Pet Shop  

Aplicação web desenvolvida em **Java (JSP/Servlets)** utilizando o padrão **MVC**, voltada ao gerenciamento de **agendamentos, cães, clientes e serviços** em um pet shop.  


## Visão Geral

O **Cão Q-Late** é um sistema web criado para simplificar o controle de **agendamentos e serviços** de um pet shop.  
Permite cadastrar, visualizar e cancelar atendimentos, respeitando regras de negócio como o **prazo mínimo de 24h** para cancelamentos.

O foco é a **organização e praticidade**, com uma interface limpa e intuitiva, e um backend sólido feito em **Java**.


## Funcionalidades Principais

**Autenticação de Administrador**  
- Login seguro (senha com hash)  
- Controle de sessão  

**Gerenciamento de Agendamentos**  
- Cadastro de novos agendamentos  
- Associação com cliente, cão e serviços  
- Cancelamento permitido apenas até 24h antes  

**Listagem Inteligente**  
- Filtro por data inicial  
- Exibe serviços agrupados por agendamento  
- Ícone de cancelamento com checagem automática  

**Interface Amigável**  
- Estilo moderno com **CSS personalizado**  
- Paleta em **dourado escuro + branco**  
- Ícones do **Bootstrap Icons**


## Arquitetura e Tecnologias

**Padrão Arquitetural:**  
Modelo **MVC (Model-View-Controller)**

**Tecnologias Principais:**
- Java 22 
- Jakarta Servlet / JSP  
- JDBC + PgAdmin 9.6 + PSQL 17 
- HTML5 / CSS3 / JS / JSTL  
- Tomcat 10.1  
- Bootstrap 


## Estrutura do Projeto
```
src/
├── br/trcs/petshop/
│ ├── dao/
│ │ ├── AdminDAO.java
│ │ ├── SchedulingDAO.java
│ │ └── ...
│ ├── logic/
│ │ ├── AuthAdmin.java
│ │ ├── DeleteScheduling.java
│ │ ├── ...
│ ├── model/
│ │ ├── Admin.java
│ │ ├── Scheduling.java
│ │ ├── Service.java
│ │ └── ...
│ ├── utils/
│ │ ├── Consts.java
│ │ └── ConnectionFactory.java
│ └── enums/
│ └── SchedulingStatus.java
└── webapp/
├── css/
│ ├── form.css
│ └── global.css
├── jsp/
│ ├── login.jsp
│ ├── show-not-finished-scheduling.jsp
│ └── ...
├── img/
│ └── favicon.ico
└── WEB-INF/
└── web.xml
```

## Configuração do Ambiente

### Requisitos
- **Java JDK 17+**  
- **Apache Tomcat 10+**  
- **MySQL 8+**  
- IDE Java (Eclipse, IntelliJ, NetBeans, etc.)

### Banco de Dados

Execute o script SQL abaixo:

```sql
CREATE DATABASE petshop;
USE petshop;

CREATE TABLE admin (
  id INT AUTO_INCREMENT PRIMARY KEY,
  email VARCHAR(100) NOT NULL,
  password VARCHAR(255) NOT NULL
);

CREATE TABLE schedulings (
  id INT AUTO_INCREMENT PRIMARY KEY,
  date DATE NOT NULL,
  cpfclient VARCHAR(20),
  iddog INT,
  status VARCHAR(20)
);

CREATE TABLE services (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(100),
  price DECIMAL(10,2)
);

CREATE TABLE scheduling_services (
  idscheduling INT,
  idservice INT,
  FOREIGN KEY (idscheduling) REFERENCES schedulings(id),
  FOREIGN KEY (idservice) REFERENCES services(id)
);
```

## Segurança e Hash de Senhas

A senha do administrador não está em texto puro no código — é armazenada como hash simples.

private static final int ADMIN_PASSWORD_HASH = "3333".hashCode();


Exemplo de resultado:

"3333".hashCode() → 1521904


No banco de dados, a senha deve ser salva já em formato de hash:

INSERT INTO admin (email, password) VALUES ('admin@petshop.com', '1569984');


## Execução do Projeto

Configure a conexão com o banco em ConnectionFactory.java:

private static final String URL = "jdbc:mysql://localhost:3306/petshop";
private static final String USER = "root";
private static final String PASSWORD = "sua_senha";


Inicie o servidor Tomcat
Acesse no navegador:

http://localhost:8080/CaoQLate/


Faça login com o administrador cadastrado
Explore as seções de agendamento, cadastro e listagem

## Capturas de Tela (opcional)
Tela	Descrição
Login	Página de autenticação do administrador
Agendamentos	Lista filtrável de agendamentos pendentes
Cancelamento	Ícone de exclusão com validação de 24h
