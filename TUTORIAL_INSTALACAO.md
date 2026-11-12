# Tutorial — Instalação do ZimaOS em Lenovo ThinkCentre Tiny

Este guia descreve um fluxo organizado para preparar um mini PC Lenovo ThinkCentre, instalar o ZimaOS e realizar a configuração inicial. O procedimento foi estruturado tomando como referência um **ThinkCentre M92p Tiny com Intel Core i5-3470T**.

> **Atenção:** as telas e opções de BIOS/UEFI variam entre gerações. Este guia não afirma que todos os modelos citados no nome do repositório foram testados. Consulte a documentação do fabricante e do ZimaOS para confirmar a compatibilidade do seu equipamento.

## 1. Antes de começar

Separe:

- Mini PC Lenovo ThinkCentre Tiny compatível.
- Monitor, teclado e mouse para a instalação inicial.
- Pendrive destinado à mídia de instalação.
- Outro computador para preparar o instalador, se necessário.
- Conexão de rede Ethernet, preferencialmente durante a configuração inicial.
- Unidade de armazenamento destinada ao sistema e/ou aos dados.

**Faça backup antes de começar.** A instalação pode apagar ou reorganizar partições e dados do disco selecionado. Desconecte unidades que não serão utilizadas, quando possível, para reduzir o risco de selecionar o disco errado.

## 2. Preparar a mídia de instalação

1. Acesse o site oficial do [ZimaOS](https://www.zimaspace.com/) e localize a versão de instalação disponibilizada pelo projeto.
2. Leia os requisitos e as instruções oficiais correspondentes à versão escolhida.
3. Baixe a imagem de instalação somente da fonte oficial.
4. Grave a imagem em um pendrive utilizando uma ferramenta compatível com gravação de imagens de disco, seguindo as instruções oficiais do ZimaOS.
5. Aguarde a conclusão da gravação e ejete o pendrive com segurança.

A gravação normalmente sobrescreve o conteúdo do pendrive. Confira se selecionou a unidade USB correta.

## 3. Conferir a BIOS/UEFI do ThinkCentre

1. Desligue completamente o mini PC.
2. Conecte o pendrive de instalação.
3. Ligue o equipamento e acesse o Setup ou o menu de inicialização usando a tecla indicada na tela do fabricante. Em muitos ThinkCentre, **F1** abre o Setup e **F12** abre o menu de boot; confirme no manual do modelo.
4. Verifique se o equipamento reconhece o pendrive.
5. Confira o modo de inicialização disponível (UEFI ou Legacy) e utilize o modo recomendado pela imagem e pela documentação da versão do ZimaOS.
6. Salve somente as alterações necessárias.

Não altere opções de firmware sem compreender o efeito. Secure Boot, modo de controladora de armazenamento e ordem de boot podem variar por geração e configuração.

## 4. Inicializar pelo pendrive

1. Reinicie o ThinkCentre com o pendrive conectado.
2. Abra o menu de boot.
3. Selecione a entrada USB correspondente ao modo de inicialização escolhido.
4. Aguarde o carregamento do instalador.
5. Siga as instruções exibidas na tela.

Se o pendrive não aparecer, teste outra porta USB, recrie a mídia e confira o modo UEFI/Legacy. Se persistir, consulte a documentação específica do modelo.

## 5. Instalar o ZimaOS

1. Leia atentamente as opções apresentadas pelo instalador.
2. Identifique pelo modelo/capacidade qual unidade será utilizada.
3. Confirme que não há dados importantes na unidade selecionada ou que o backup foi validado.
4. Selecione o destino e prossiga conforme as instruções da versão instalada.
5. Aguarde a conclusão. Não desligue o equipamento durante a gravação.
6. Quando solicitado, remova o pendrive e reinicie.

> Os nomes das opções e o particionamento podem mudar entre versões. Este tutorial não fixa tamanhos de partição nem recomenda comandos destrutivos: siga o instalador oficial para a versão em uso.

## 6. Primeiro acesso e configuração inicial

1. Conecte o servidor à rede local, preferencialmente por cabo Ethernet.
2. Aguarde a inicialização completa.
3. Identifique o endereço IP atribuído pelo roteador ou pelo próprio ambiente de rede.
4. Em outro dispositivo da mesma rede, abra o endereço ou método de acesso indicado pelo ZimaOS.
5. Conclua o assistente inicial, defina credenciais seguras e confira as configurações de rede.
6. Registre o endereço reservado para o servidor no roteador, se desejar manter um endereço estável.

Não exponha o painel administrativo diretamente à internet. Para acesso remoto, utilize uma solução segura e autenticada.

## 7. Armazenamento e aplicações

Antes de instalar aplicações:

- Confira se os discos aparecem corretamente no painel.
- Identifique quais unidades serão destinadas ao sistema e aos dados.
- Defina uma estratégia de backup independente do disco principal.
- Mantenha espaço livre para atualizações, imagens de contêineres e dados das aplicações.

O ZimaOS pode hospedar aplicações em contêineres. A disponibilidade e o método de instalação dependem do catálogo, da versão e da configuração do sistema. Revise volumes persistentes, portas de rede, permissões e políticas de atualização de cada aplicação.

## 8. Exemplo de serviços do projeto

Na instalação de referência deste projeto, o servidor foi utilizado como base para serviços como:

- **Home Assistant:** automação residencial e interface Lovelace.
- **Mosquitto MQTT:** comunicação entre dispositivos e integrações.
- **Glances:** monitoramento de recursos do servidor.
- **Frigate:** gerenciamento e análise de câmeras, conforme os recursos disponíveis.
- **AdGuard Home:** serviço de DNS e filtragem de rede.
- **Immich e Stremio:** aplicações adicionais, conforme necessidade.

Esta relação descreve serviços utilizados no ambiente de referência, não uma lista obrigatória. Instale apenas o que pretende utilizar e avalie consumo de memória, processador e armazenamento.

## 9. Integração com a dashboard Central da Casa

O projeto de automação residencial associado a este servidor está documentado em outro repositório:

**[Dashboard Home Assistant — Central da Casa](https://github.com/Douglas-TADS/Dashboard-Home-Assistant)**

A dashboard foi desenvolvida para apresentar controles residenciais, câmeras, conectividade e indicadores do servidor. Ela depende de uma instalação Home Assistant funcional e das integrações/entidades correspondentes.

O repositório da dashboard contém o YAML completo, documentação própria e uma ilustração conceitual. A configuração de cada instalação pode exigir adaptação dos IDs de entidades, endereços e serviços.

## 10. Diagnóstico e recuperação

### O pendrive não aparece no menu de boot
- Recrie a mídia a partir da imagem oficial.
- Teste outra porta USB.
- Confira se a entrada UEFI/Legacy corresponde ao modo utilizado na gravação.
- Consulte o manual do modelo.

### O equipamento não inicializa após a instalação
- Remova o pendrive e confira a ordem de boot.
- Verifique se a unidade de destino é detectada na BIOS/UEFI.
- Revise alterações recentes de firmware.
- Evite formatar ou reinstalar antes de avaliar se há dados que precisam ser recuperados.

### Erro de inicialização ou mensagem semelhante a “Error 1962”
Esse tipo de mensagem está relacionado ao processo de inicialização e pode ter diferentes causas. Confira primeiro a detecção do disco, a ordem de boot e o modo UEFI/Legacy. Não execute comandos de reparo de boot encontrados na internet sem compreender o efeito e sem ter backup.

## 11. Manutenção recomendada

- Aplique atualizações do ZimaOS após ler as notas da versão.
- Mantenha backups dos dados persistentes das aplicações.
- Monitore temperaturas, memória, armazenamento e estado dos contêineres.
- Documente alterações de BIOS/UEFI e de rede.
- Teste periodicamente a restauração dos backups.

## 12. Informações para relatar compatibilidade

Ao testar outro ThinkCentre, registre:

| Informação | Exemplo / observação |
|---|---|
| Modelo exato | M92p Tiny, M720q, M920q etc. |
| Processador | Modelo completo |
| Memória RAM | Capacidade instalada |
| Armazenamento | Tipo, capacidade e interface |
| BIOS/UEFI | Versão instalada |
| Inicialização | UEFI ou Legacy |
| ZimaOS | Versão instalada |
| Resultado | Instalou, iniciou e reconheceu os dispositivos? |

Esses dados ajudam a separar configurações efetivamente testadas de modelos apenas considerados como possíveis alvos.

---

**Documentação oficial:** [ZimaOS](https://www.zimaspace.com/) · [Documentação Zima](https://www.zimaspace.com/docs)  
**Projeto relacionado:** [Central da Casa — Home Assistant](https://github.com/Douglas-TADS/Dashboard-Home-Assistant)  
**Autor:** Douglas TADS · **Idioma:** Português (Brasil)
