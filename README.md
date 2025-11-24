# 🖨️ Sistema de Impressão via JNA

## 📌 Linguagem Utilizada
- Java

## 🛠️ Ferramentas Utilizadas
- **IntelliJ IDEA Community Edition**  
- **JDK 25**

## 📚 Biblioteca Utilizada
- **E1_impressora01.dll**  
  - Biblioteca dinâmica fornecida pela **Elgin** para integração com impressoras térmicas.  
  - Responsável por disponibilizar funções nativas que permitem:  
    - Abrir e fechar conexões com a impressora.  
    - Imprimir textos, QR Codes, códigos de barras e XMLs do SAT.  
    - Controlar periféricos como gaveta de dinheiro e sinal sonoro.  
    - Executar cortes de papel após a impressão.  
  - Foi integrada ao projeto via **JNA**, permitindo que o Java chamasse diretamente as funções da DLL.  
  - É o **coração da comunicação** entre o sistema e a impressora, garantindo que os comandos enviados pelo usuário sejam traduzidos corretamente para o hardware.  

## 👥 Integrantes do Grupo
- Arthur Fernandes  
- Caio Damasceno  
- Emilly Nayara  
- Luiza Rocha  

---

## 🚀 O que o grupo desenvolveu
Nosso grupo ficou responsável por montar a parte principal do sistema que permite que o usuário escolha ações no terminal e envie comandos para a impressora através da DLL usando **JNA**.

### Partes feitas:
- **Integração com a impressora (via JNA)**  
- **Menu interativo no terminal**  
- **Estrutura switch-case**  

---

## 🔧 Observação
A parte que fizemos garante o fluxo completo:  
**entrada do usuário → validação → chamada da função da DLL → retorno e mensagem para o usuário.**

---

## 📖 Explicação das funções
- **configurarConexao()** → Lê tipo, modelo, conexão e parâmetro da impressora e guarda para uso posterior.  
- **abrirConexao()** → Abre a comunicação com a impressora via `AbreConexaoImpressora`.  
- **fecharConexao()** → Fecha a comunicação com a impressora via `FechaConexaoImpressora`.  
- **impressaoTexto()** → Imprime texto simples com posição, estilo e tamanho.  
- **corte()** → Realiza o corte do papel.  
- **impressaoQRCode()** → Imprime QR Code com conteúdo, tamanho e nível de correção.  
- **impressaoCodigoBarras()** → Imprime código de barras com tipo, dados, altura, largura e HRI.  
- **abreGavetaElgin() / abreGaveta()** → Abrem a gaveta de dinheiro conectada à impressora.  
- **SinalSonoro()** → Faz a impressora emitir beep como aviso sonoro.  
- **ImprimeXMLSAT() / ImprimeXMLCancelamentoSAT()** → Imprime XMLs do SAT (nota fiscal).  

---

## 📝 Como funciona o menu com switch-case (passo a passo)

1. O programa mostra o menu com todas as opções.  
2. O usuário digita o número da ação desejada.  
3. A entrada é lida pelo programa.  
4. O `switch-case` verifica qual foi o número digitado.  
5. O `case` correspondente chama a função correta.  
6. A função acessa a DLL, executa e mostra se deu certo ou não.  
7. O menu aparece novamente.  
8. O programa só encerra quando o usuário digita **0**.  

---
