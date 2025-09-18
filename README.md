# Senior Developer Technical Assessment - Debugging & Code Review

Este repositório contém a minha análise para o teste técnico de Desenvolvedor Sênior. O objetivo era revisar dois blocos de código (Java e C#), identificar problemas e sugerir melhorias.

---

## Estrutura do repositório

- `/java` → código original fornecido em Java.  
- `/c#` → código original fornecido em C#.  
- `README.md` → análise e apontamentos.

---

## Análise - Java

### Problemas identificados
1. **Concorrência no uso da lista**  
   - O ArrayList não é thread-safe, mas está sendo acessado por múltiplas threads.  
   - Isso pode gerar inconsistências e comportamento inesperado.

2. **Reabertura de arquivo em cada thread**  
   - Cada thread abre o mesmo arquivo data.txt.  

3. **Gerenciamento de recursos**  
   - O BufferedReader é fechado manualmente, sem try-with-resources, podendo ocasionar vazamento de memória em caso de exceção.  

4. **Execução assíncrona mal controlada**  
   - O executor.shutdown() é chamado, mas não há awaitTermination, logo o programa pode encerrar antes das threads terminarem.

---

## Análise C#

### Problemas identificados
1. **Concorrência no acesso ao cache**  
   - O List<string> não é thread-safe, mas está sendo acessado por múltiplas threads.

2. **Tasks não aguardadas**  
   - O método DownloadAsync é chamado sem await dentro do loop, logo o programa segue sem aguardar o término dos downloads.

3. **Criação de HttpClient em cada requisição**  
   - Um HttpClient é instanciado em cada chamada, em vez de usar uma instância única e reutilizável.

4. **Resultado inconsistente no cache**  
   - Como não aguarda as tasks finalizarem, o valor de cache.Count provavelmente será inconsistente.

---
