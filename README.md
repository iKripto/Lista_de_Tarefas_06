# Lista de Tarefas 06 — Spring Boot + Vue.js

## Autor
**Yago Nascimento**

---

## 1. Problema Encontrado
os dados de seed não estavam sendo carregados porque o backend bloqueava o acesso do frontend devido à configuração de **CORS**.

---

## 2. Correção Realizada

### Backend (Spring Boot)
Foi adicionada a configuração de **CORS** para permitir o acesso do frontend à API:

```java
@Configuration
public class WebConfig {
    @Bean
    public WebMvcConfigurer corsConfigurer() {
        return new WebMvcConfigurer() {
            @Override
            public void addCorsMappings(CorsRegistry registry) {
                registry.addMapping("/**")
                        .allowedOrigins("http://localhost:5173")
                        .allowedMethods("GET", "POST", "PUT", "DELETE");
            }
        };
    }
}
```

Com isso, o frontend consegue acessar os dados do backend normalmente, sem erros de CORS.

### Frontend (Vue.js)
Foi ajustado o componente responsável por exibir os títulos das tarefas:

```html
<span v-if="tarefaEditandoId !== tarefa.id">
  {{ tarefa.titulo }}
</span>
```

Agora os títulos são exibidos corretamente e a lista funciona como esperado.

---

## 3. Como Executar o Projeto

### Backend
1. Abra o projeto Spring Boot na sua IDE.  
2. Execute a classe **ApiApplication.java**.  
3. A API ficará disponível em:  
   ```
   http://localhost:8088/api
   ```

### Frontend
1. Acesse a pasta do projeto Vue.  
2. Instale as dependências:  
   ```
   npm install
   ```
3. Inicie o servidor:  
   ```
   npm run dev
   ```
4. Acesse o sistema no navegador:  
   ```
   http://localhost:5173
   ```

---

## 4. Funcionalidades Corrigidas
- Listagem de tarefas  
- Adição de novas tarefas  
- Edição de títulos  
- Marcação de tarefas concluídas  
- Remoção de tarefas  
- Comunicação entre frontend e backend funcionando corretamente  