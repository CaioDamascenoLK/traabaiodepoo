README – Sistema de Impressão via JNA
Linguagem Utilizada
Java
Integrantes do Grupo
Arthur Fernandes
Caio Damasceno
Emilly Nayara
Luiza Rocha
O que o grupo desenvolveu
Nosso grupo ficou responsável por montar a parte principal do sistema que permite que o usuário escolha ações no terminal e envie comandos para a impressora através da DLL usando JNA.
As partes feitas foram:
 Integração com a impressora (via JNA)
Fizemos a ligação do Java com a DLL da impressora usando JNA.
A DLL é carregada direto no código.
Menu interativo no terminal
Criamos um menu simples, onde o usuário digita números para escolher o que quer fazer (como abrir conexão, imprimir texto, cortar papel, etc.).
Esse menu facilita o uso sem precisar de interface gráfica.
Estrutura switch-case
Usamos um switch-case para organizar as opções digitadas pelo usuário.
Cada opção chama uma função diferente (por exemplo, opção 3 → imprimir texto → depois cortar papel).
Isso deixa o fluxo do programa organizado e evita erros de chamar função errada.
Observação
A parte que fizemos garante o fluxo completo: 
 entrada do usuário → validação → chamada da função da DLL → retorno e mensagem para o usuário.
Explicação das funções que usamos
configurarConexao()
Serve para pegar do usuário as informações necessárias para conectar na impressora.
Ela lê tipo, modelo, conexão e parâmetro e guarda para depois.
Usada antes de abrir de fato a conexão.
abrirConexao()
Abre a comunicação com a impressora.
Chama AbreConexaoImpressora da DLL com os dados configurados.
Verifica o retorno e marca se a conexão está aberta ou não.
fecharConexao()
Fecha a comunicação com a impressora.
Chama FechaConexaoImpressora e atualiza o estado da conexão.
impressaoTexto()
Imprime um texto simples.
Usa a função ImpressaoTexto passando posição, estilo e tamanho.
Na maioria das vezes, é chamada junto com o corte depois.
corte()
Realiza o corte do papel.
No nosso código, às vezes é chamada direto depois da impressão.
impressaoQRCode()
Imprime um QR Code.
Usa ImpressaoQRCode passando o conteúdo, tamanho e nível de correção.
impressaoCodigoBarras()
Imprime código de barras.
Usa ImpressaoCodigoBarras com tipo, dados, altura, largura e HRI.
abreGavetaElgin() e abreGaveta()
Abrem a gaveta de dinheiro conectada à impressora.
Uma delas é específica para impressoras Elgin, a outra permite configurar pino e tempo.
SinalSonoro()
Faz a impressora emitir um beep.
Serve como aviso sonoro para alguma ação.
ImprimeXMLSAT() e ImprimeXMLCancelamentoSAT()
Imprimem XMLs do SAT (nota fiscal).
Uma para a venda e outra para o cancelamento.
Como funciona o menu com o switch-case (passo a passo)
O programa mostra o menu com todas as opções.
O usuário digita o número da ação que quer executar.
A entrada é lida pelo programa.
O switch-case verifica qual foi o número digitado.
O case correspondente chama a função certa.
A função acessa a DLL, executa e mostra se deu certo ou não.
Quando termina, o menu aparece de novo.
O programa só encerra quando o usuário digita 0.

