# Especificações dos casos de uso

## UC01 – Validar acesso

| Campo | Conteúdo |
|---|---|
| Nome | Validar acesso |
| Número | UC01 |
| Descrição | Valida, em tempo real, a leitura de carteirinha ou biometria e libera ou nega o acesso, registrando a tentativa. |
| Atores | Aluno/Funcionário (principal); Vigilante/Porteiro (secundário) |
| Pré-requisitos | Dispositivo operante e cadastrado; usuário com carteirinha ou biometria cadastrada. |
| Fluxo principal | 1. O usuário apresenta a carteirinha ou a digital ao leitor.<br>2. O leitor envia a leitura ao sistema (UC02).<br>3. O sistema identifica o usuário e verifica o cadastro, a carteirinha e a permissão no local (UC03).<br>4. O sistema libera o acesso.<br>5. O sistema emite o alerta de acesso liberado (UC04).<br>6. O sistema registra a tentativa. |
| Fluxos alternativos | A1 – Leitura inválida ou usuário não registrado: exibe ERRO DE LEITURA, orienta contato com um responsável e registra o erro.<br>A2 – Vínculo inativo ou carteirinha vencida/bloqueada: nega o acesso e registra o motivo.<br>A3 – Sem permissão no local: nega o acesso e registra o motivo. |
| Pós-condições | Tentativa registrada; alerta exibido ao usuário e ao vigilante. |
| Requisitos e regras | RF001–RF006, RF008, RF009; RN001–RN004, RN010 |

## UC02 – Ler carteirinha ou biometria

| Campo | Conteúdo |
|---|---|
| Nome | Ler carteirinha ou biometria |
| Número | UC02 |
| Descrição | Captura o código de barras da carteirinha ou a impressão digital e a envia ao sistema. |
| Atores | Aluno/Funcionário |
| Pré-requisitos | Leitor ligado à rede e com status operante. |
| Fluxo principal | 1. O usuário aproxima a carteirinha ou posiciona o dedo no leitor.<br>2. O leitor captura o código ou a amostra biométrica.<br>3. O leitor envia o dado, com o identificador do dispositivo, ao SAGA. |
| Fluxos alternativos | A1 – Falha de captura: o leitor solicita nova tentativa e, após três falhas, o sistema registra erro de leitura. |
| Pós-condições | Leitura entregue ao controle de acesso. |
| Requisitos e regras | RF001, RF002 |

## UC03 – Verificar vínculo e permissão

| Campo | Conteúdo |
|---|---|
| Nome | Verificar vínculo e permissão |
| Número | UC03 |
| Descrição | Consulta o cadastro, o status do vínculo, a validade da carteirinha e a permissão do perfil no local. |
| Atores | Sistema (ator de apoio: Secretaria Acadêmica, que mantém o cadastro) |
| Pré-requisitos | Leitura recebida e identificada. |
| Fluxo principal | 1. O sistema busca o usuário pelo código ou pela biometria.<br>2. Verifica status ativo e data de vencimento do vínculo.<br>3. Verifica a situação e a validade da carteirinha.<br>4. Consulta a permissão do perfil para o local do dispositivo.<br>5. Devolve o resultado (liberado ou negado, com motivo). |
| Fluxos alternativos | A1 – Usuário não encontrado: resultado = erro de leitura. |
| Pós-condições | Resultado da validação disponível. |
| Requisitos e regras | RF003, RF004, RF008; RN001, RN003, RN004 |

## UC04 – Emitir alerta visual e sonoro

| Campo | Conteúdo |
|---|---|
| Nome | Emitir alerta visual e sonoro |
| Número | UC04 |
| Descrição | Exibe e toca o retorno do resultado ao usuário e ao vigilante. |
| Atores | Vigilante/Porteiro; Aluno/Funcionário |
| Pré-requisitos | Resultado da validação disponível. |
| Fluxo principal | 1. O sistema escolhe o tipo de alerta (liberado, negado ou erro).<br>2. Exibe a tela correspondente (verde para liberado; vermelha para negado e erro) com nome, foto e ocupação quando houver usuário.<br>3. Toca o som associado ao resultado. |
| Fluxos alternativos | A1 – Dispositivo de saída indisponível: o alerta aparece apenas no painel do vigilante. |
| Pós-condições | Usuário e vigilante informados do resultado. |
| Requisitos e regras | RF009 |

## UC05 – Monitorar acessos em tempo real

| Campo | Conteúdo |
|---|---|
| Nome | Monitorar acessos em tempo real |
| Número | UC05 |
| Descrição | Exibe, no painel, as últimas entradas e saídas com contadores do dia. |
| Atores | Vigilante/Porteiro; Coord. de Segurança |
| Pré-requisitos | Operador autenticado. |
| Fluxo principal | 1. O operador abre a Tela Inicial.<br>2. O sistema lista os registros recentes (nome, ocupação, dispositivo, local, data e hora).<br>3. O sistema atualiza a lista e os contadores de entradas e saídas a cada novo registro. |
| Fluxos alternativos | A1 – Sem conexão com o servidor: exibe aviso de painel desatualizado. |
| Pós-condições | Painel atualizado. |
| Requisitos e regras | RF020; RNF001 |

## UC06 – Gerar relatórios

| Campo | Conteúdo |
|---|---|
| Nome | Gerar relatórios |
| Número | UC06 |
| Descrição | Gera relatórios personalizados de acesso. |
| Atores | Coord. de Segurança; Diretoria Acadêmica |
| Pré-requisitos | Operador autenticado com papel de Segurança ou Diretoria. |
| Fluxo principal | 1. O operador abre Relatórios Personalizados.<br>2. Informa dispositivo, local e período.<br>3. O sistema consulta os registros e exibe a tabela.<br>4. O operador exporta o relatório, se desejar. |
| Fluxos alternativos | A1 – Nenhum registro no filtro: exibe mensagem de resultado vazio. |
| Pós-condições | Relatório exibido/exportado. |
| Requisitos e regras | RF010; RN009 |

## UC07 – Gerenciar usuários

| Campo | Conteúdo |
|---|---|
| Nome | Gerenciar usuários |
| Número | UC07 |
| Descrição | Cadastra, consulta, altera e inativa usuários, incluindo foto, código de barras e biometria. |
| Atores | Secretaria Acadêmica |
| Pré-requisitos | Operador autenticado com papel de Secretaria. |
| Fluxo principal | 1. O operador abre Usuários e informa o CPF.<br>2. O sistema consulta o CPF; se novo, abre o formulário.<br>3. O operador informa dados pessoais e acadêmicos, foto, código de barras e biometria.<br>4. O operador define tipo de usuário, perfil e status.<br>5. O sistema valida os campos obrigatórios, salva e registra a auditoria. |
| Fluxos alternativos | A1 – CPF já cadastrado: carrega os dados para edição.<br>A2 – Campos obrigatórios inválidos: indica os erros e não salva. |
| Pós-condições | Usuário salvo e disponível para validação de acesso. |
| Requisitos e regras | RF011, RF014–RF016, RF019, RF021, RF022; RN005, RN006, RN008 |

## UC08 – Gerenciar perfis e permissões

| Campo | Conteúdo |
|---|---|
| Nome | Gerenciar perfis e permissões |
| Número | UC08 |
| Descrição | Define perfis de acesso e os locais permitidos a cada perfil. |
| Atores | Coord. de Segurança |
| Pré-requisitos | Operador autenticado com papel de Segurança. |
| Fluxo principal | 1. O operador abre a gestão de perfis.<br>2. Cria ou edita um perfil.<br>3. Seleciona os locais permitidos.<br>4. O sistema salva e aplica as permissões às próximas validações. |
| Fluxos alternativos | A1 – Perfil em uso por usuários: impede a exclusão e sugere inativação. |
| Pós-condições | Permissões atualizadas. |
| Requisitos e regras | RF007, RF008, RF013; RN003, RN008 |

## UC09 – Gerenciar dispositivos

| Campo | Conteúdo |
|---|---|
| Nome | Gerenciar dispositivos |
| Número | UC09 |
| Descrição | Cadastra e acompanha os leitores (modelo, número de série, status e local). |
| Atores | TI/Infraestrutura |
| Pré-requisitos | Operador autenticado com papel de TI; local cadastrado. |
| Fluxo principal | 1. O operador abre Dispositivos.<br>2. Informa modelo, número de série, status e local.<br>3. O sistema salva e atualiza os indicadores de dispositivos operantes e não operantes. |
| Fluxos alternativos | A1 – Número de série duplicado: rejeita o cadastro. |
| Pós-condições | Dispositivo cadastrado e monitorado. |
| Requisitos e regras | RF012; RN007 |

## UC10 – Gerenciar locais de acesso

| Campo | Conteúdo |
|---|---|
| Nome | Gerenciar locais de acesso |
| Número | UC10 |
| Descrição | Cadastra locais e seus tipos (sala, laboratório, portão, biblioteca). |
| Atores | TI/Infraestrutura |
| Pré-requisitos | Operador autenticado com papel de TI. |
| Fluxo principal | 1. O operador abre o cadastro de locais.<br>2. Informa o nome do local e o seu tipo.<br>3. O sistema salva e disponibiliza o local para dispositivos e permissões. |
| Fluxos alternativos | A1 – Nome duplicado: rejeita o cadastro. |
| Pós-condições | Local disponível. |
| Requisitos e regras | RF017, RF018 |
