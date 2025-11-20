README – Sistema de Impressão via JNA
 Linguagem Utilizada
Java
Integrantes do Grupo (ordem alfabética)
Arthur Fernandes
Caio Damasceno
Emilly Nayara
Luiza Rocha
O que o grupo desenvolveu 
O grupo implementou as partes principais responsáveis por permitir que um usuário selecione ações no terminal e envie comandos para a impressora. As tarefas realizadas foram:
Conexão com a impressora (via JNA)
Fizemos a integração com a DLL da impressora usando JNA.
Carregamos diretamente o arquivo da DLL no código.
Menu interativo no terminal
Criamos um menu textual que é exibido ao usuário com opções numeradas (ex.: configurar conexão, abrir conexão, imprimir texto, etc.).
O menu facilita o uso manual do sistema sem interface gráfica avançada.
Estrutura switch-case que chama as funções
Implementamos um switch-case que recebe a opção digitada pelo usuário e chama a função correspondente.
Cada case mapeia diretamente para uma ação (por exemplo, opção 3 chama a função de impressão de texto e em seguida executa o corte de papel).
Essa estrutura organiza o fluxo do programa e garante que somente uma ação por vez seja executada.
Observação: o grupo cuidou da ligação entre o menu (entrada do usuário) e as funções da biblioteca, ou seja, do fluxo completo: receber opção -> validar -> chamar função nativa -> tratar retorno.
Explicação detalhada das funções implementadas
Abaixo está a descrição do propósito e do comportamento de cada função usada no sistema.
configurarConexao()
Finalidade: coletar do usuário os parâmetros necessários para a conexão com a impressora.
O que faz: lê tipo, modelo, conexao e parametro via terminal e os armazena (para uso quando a conexão for aberta).
Observação: é a etapa inicial antes de chamar abrirConexao().
abrirConexao()
Finalidade: estabelecer a comunicação com a impressora.
O que faz: chama a função da DLL (AbreConexaoImpressora) passando os parâmetros coletados; verifica o código de retorno e seta uma variável conexaoAberta para controlar o estado.
Tratamento: exibe mensagens de sucesso/erro dependendo do retorno.
fecharConexao()
Finalidade: encerrar a sessão com a impressora.
O que faz: chama FechaConexaoImpressora e atualiza o estado conexaoAberta conforme o retorno.
impressaoTexto()
Finalidade: enviar texto simples para impressão.
O que faz: utiliza ImpressaoTexto da DLL com parâmetros de posição/estilo/tamanho; trata o retorno e informa ao usuário.
Observação: normalmente utilizada junto com o comando de Corte() após a impressão.
corte()
Finalidade: realizar o corte do papel.
O que faz: envia comando Corte para a impressora (usada após impressões). No código atual, a função existe como placeholder ou o corte é chamado diretamente após as impressões.
impressaoQRCode()
Finalidade: gerar e imprimir um QR Code.
O que faz: chama ImpressaoQRCode na DLL com dados, tamanho e nível de correção; valida retorno.
impressaoCodigoBarras()
Finalidade: gerar e imprimir um código de barras (ex.: EAN/Code128 dependendo do tipo).
O que faz: chama ImpressaoCodigoBarras com tipo, dados, altura, largura e HRI; trata erros e confirma impressão.
avancaPapel()
Finalidade: avançar o papel algumas linhas após a impressão.
O que faz: chama AvancaPapel e verifica o sucesso do comando.
abreGavetaElgin() e abreGaveta()
Finalidade: abrir a gaveta de dinheiro (caixa) conectada à impressora.
O que faz: AbreGavetaElgin() usa um comando padrão específico de algumas impressoras Elgin; AbreGaveta() permite passar pino e tempos personalizados.
SinalSonoro()
Finalidade: emitir um sinal sonoro (beep) pela impressora.
O que faz: chama SinalSonoro com quantidade e tempos, útil para alertas de operação.
ImprimeXMLSAT() e ImprimeXMLCancelamentoSAT()
Finalidade: imprimir XMLs relacionados ao SAT (sistema de nota fiscal eletrônica) — tanto o XML de venda quanto o de cancelamento.
O que faz: envia o caminho do arquivo XML (ou o conteúdo conforme implementação) para as funções ImprimeXMLSAT / ImprimeXMLCancelamentoSAT da DLL.
Como o menu e o switch-case atuam no fluxo do programa (passo a passo)
O programa exibe o menu com opções numeradas.
O usuário digita o número referente à ação desejada.
O capturarEntrada() lê a entrada como String.
O switch-case avalia essa string e direciona para o case correspondente.
Cada case chama a função apropriada (ex: impressaoTexto()), e alguns cases também chamam comandos de apoio em sequência (ex: Corte() logo após a impressão).
A função executada chama a função nativa da DLL, verifica o retorno e imprime mensagens de resultado (sucesso/erro).
O menu reaparece, permitindo novas operações até que o usuário escolha 0 para fechar a conexão e sair.
