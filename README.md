# MS-EurekaServer-Application

## Visão Geral
A **MS-EurekaServer-Application** é um servidor Eureka desenvolvido com Spring Boot e Netflix Eureka. Ele atua como um service registry (registro de serviços) em uma arquitetura de microsserviços, permitindo que outras aplicações descubram e se comuniquem dinamicamente.

## Tecnologias Utilizadas
- **Java** (versão recomendada: 17+)
- **Spring Boot**
- **Spring Cloud Netflix Eureka**
- **Maven**

## Estrutura do Projeto

```
MS-EurekaServer-Application/
│── src/
│   ├── main/
│   │   ├── java/com/MS/EurekaServer/Application/EurekaServer/
│   │   │   ├── EurekaServerApplication.java
│   ├── resources/
│   │   ├── application.yml
│── pom.xml
│── README.md
```

## Configuração da Aplicação
A classe principal da aplicação **EurekaServerApplication**:

```java
package com.MS.EurekaServer.Application.EurekaServer;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.netflix.eureka.server.EnableEurekaServer;

// Configuração simples do servidor Eureka
@SpringBootApplication
@EnableEurekaServer
public class EurekaServerApplication {
    public static void main(String[] args) {
        SpringApplication.run(EurekaServerApplication.class, args);
    }
}
```

A anotação `@EnableEurekaServer` habilita este projeto como um servidor Eureka.

## Configuração do application.yml
Para configurar corretamente o Eureka Server, utilize um arquivo `application.yml`:

```yaml
spring:
  application:
    name: eurekaserver

server:
  port: 8761

eureka:
  client:
    register-with-eureka: false
    fetch-registry: false
```

- **Nome da aplicação**: `eurekaserver`, usado para identificação no registro.
- **Porta**: O servidor está configurado para rodar na porta `8761`.
- **register-with-eureka**: Falso, pois este é o servidor e não precisa se registrar.
- **fetch-registry**: Falso, pois ele não precisa buscar registros.

## Configuração do pom.xml
O `pom.xml` define as dependências e versões utilizadas no projeto:

```xml
<properties>
    <java.version>17</java.version>
    <spring-cloud.version>2023.0.2</spring-cloud.version>
</properties>

<dependencies>
    <!-- Spring Cloud Netflix Eureka Server -->
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
    </dependency>
    <!-- Spring Boot Starter Test -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>
</dependencies>

<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-dependencies</artifactId>
            <version>${spring-cloud.version}</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

- **Java 17**: Versão recomendada para compatibilidade com Spring Boot 3.
- **Spring Cloud 2023.0.2**: Versão utilizada para os serviços do Eureka.
- **Dependência do Eureka Server**: Necessária para habilitar o registro de serviços.

## Como Executar
1. Certifique-se de ter o JDK instalado.
2. Clone o repositório e navegue até a pasta do projeto.
3. Execute o seguinte comando:
   ```sh
   mvn spring-boot:run
   ```
4. Acesse a interface do Eureka Server no navegador:
   ```
   http://localhost:8761
   ```

## Possíveis Problemas e Soluções
- **Problema: O Eureka Server não inicia corretamente**
  - Solução: Verifique se a porta 8761 está livre e se as dependências no `pom.xml` estão corretas.

- **Problema: Aplicativos clientes não conseguem se registrar**
  - Solução: Confirme se os clientes estão configurados corretamente para apontar para o servidor Eureka.

## Conclusão
A **MS-EurekaServer-Application** é um servidor central para registros de serviços em um ecossistema de microsserviços. Sua implementação é simples e eficaz para arquiteturas distribuídas.