

Manual das APIs de

Consultas



PNCP



Portal Nacional de Contratações Públicas


Sumário





# 


# 1. Objetivo

Este documento contempla as orientações para consultas aos dados de contratações, alienação de bens móveis e imóveis, atas de registro de preços e contratos realizados no âmbito da Lei n° 14.133/2021.

# 2. Protocolo de Comunicação

As consultas serão realizadas por meio de API (Application Programme Interface) que utiliza o protocolo de comunicação REST - Representational State Transfer/ HTTP 1.1 cujos dados trafegados utilizam a notação JSON - JavaScript Object Notation.

# 3. Acesso ao PNCP

## 3.1. Endereços de Acesso

A invocação dos serviços será realizada através das URLs citadas abaixo, conforme requisitos de segurança detalhados na seção seguinte.



Ambiente de Produtivo



Portal: 

Documentação Técnica (Serviços): https://pncp.gov.br/api/consulta/swagger-ui/index.html

Serviços (${BASE_URL}): 

Nota: ${BASE_URL} será utilizada nos exemplos de requisições citados neste documento. É a URL base para acesso aos serviços disponíveis no PNCP.

# 4. Recomendações Iniciais

## 4.1. Composição do Número de Controle PNCP de PCA/Contratação/Ata/Contrato

O PNCP gera automaticamente um identificador, que é um número de controle, no qual utiliza-se para reconhecer todas as demais transações realizadas para aquele registro.

Atualmente encontram-se disponíveis: plano de contratações anual (PCA), contratação (licitação ou contratação direta), ata de registro de preços ou contrato, conforme a composição abaixo:

Número de Controle do PCA (id pca pncp)  (Máscara 99999999999999-0-999999/9999.)

Cada PCA receberá um número de controle composto por:

CNPJ do Órgão/Entidade do PCA (14 dígitos)

Dígito "0" - marcador que indica tratar-se de um plano de contratação anual

Número sequencial do Plano no PNCP*

Ano do Plano (4 dígitos)

Número de Controle da Contratação (id contratação pncp)  (Máscara: 99999999999999-1-999999/9999.)

Cada contratação receberá um número de controle composto por:

CNPJ do Órgão/Entidade da contratação (14 dígitos)

Dígito "1" - marcador que indica tratar-se de uma contratação

Número sequencial da contratação no PNCP  *

Ano da contratação (4 dígitos)

Número de Controle da Ata (id ata pncp)  (Máscara: 99999999999999-1-999999/9999-999999.)

Cada ata receberá um número de controle composto por:

Número de Controle PNCP da Contratação (24 dígitos)

Número sequencial da ata no PNCP  *

Número de Controle do Contrato (id contrato pncp)  (Máscara: 99999999999999-2-999999/9999.)

Cada contrato receberá um número de controle composto por:

CNPJ do Órgão/Entidade do Contrato (14 dígitos)

Dígito "2" - marcador que indica tratar-se de um contrato

Número sequencial do contrato no PNCP  *

Ano do contrato (4 dígitos)

*  O número PNCP será gerado sequencialmente com 6 dígitos e reiniciado a cada mudança de ano.

# 5. Tabelas de Domínio

A seguir são encontradas informações sobre as tabelas de domínio que são listas predefinidas em bancos de dados que armazenam valores fixos, usados frequentemente em várias partes de uma aplicação. Elas garantem consistência ao limitar as opções de entrada. 



Para uso de algumas APIs pode ser necessário incluir o Identificador Único do portal ou sistema integrado (idUsuario). Essa informação pode ser encontrada acessando o sítio:  e clicando em “Pesquisa ID” conforme imagem a seguir:







## 5.1. Instrumento Convocatório



(código = 1) Edital: Instrumento convocatório utilizado no diálogo competitivo, concurso, concorrência, pregão, manifestação de interesse, pré-qualificação e credenciamento.

(código = 2) Aviso de Contratação Direta: Instrumento convocatório utilizado na Dispensa com Disputa.

(código = 3) Ato que autoriza a Contratação Direta: Instrumento convocatório utilizado na Dispensa sem Disputa ou na Inexigibilidade.



## 5.2. Modalidade de Contratação



(código = 1) Leilão - Eletrônico

(código = 2) Diálogo Competitivo

(código = 3) Concurso

(código = 4) Concorrência - Eletrônica

(código = 5) Concorrência - Presencial

(código = 6) Pregão - Eletrônico

(código = 7) Pregão - Presencial

(código = 8) Dispensa de Licitação

(código = 9) Inexigibilidade

(código = 10) Manifestação de Interesse

(código = 11) Pré-qualificação

(código = 12) Credenciamento

(código = 13) Leilão - Presencial



## 5.3. Modo de Disputa



(código = 1) Aberto

(código = 2) Fechado

(código = 3) Aberto-Fechado

(código = 4) Dispensa Com Disputa

(código = 5) Não se aplica

(código = 6) Fechado-Aberto



## 5.4. Critério de Julgamento



(código = 1) Menor preço

(código = 2) Maior desconto

(código = 4) Técnica e preço

(código = 5) Maior lance

(código = 6) Maior retorno econômico

(código = 7) Não se aplica

(código = 8) Melhor técnica

(código = 9) Conteúdo artístico



## 5.5. Situação da Contratação



(código = 1) Divulgada no PNCP: Contratação divulgada no PNCP. Situação atribuída na inclusão da contratação.

(código = 2) Revogada: Contratação revogada conforme justificativa.

(código = 3) Anulada: Contratação revogada conforme justificativa.

(código = 4) Suspensa: Contratação suspensa conforme justificativa.



## 5.6. Situação do Item da Contratação



(código = 1) Em Andamento: Item com disputa/seleção do fornecedor/arrematante não finalizada. Situação atribuída na inclusão do item da contratação

(código = 2) Homologado: Item com resultado (fornecedor/arrematante informado)

(código = 3) Anulado/Revogado/Cancelado: Item cancelado conforme justificativa

(código = 4) Deserto: Item sem resultado (sem fornecedores/arrematantes interessados)

(código = 5) Fracassado: Item sem resultado (fornecedores/arrematantes desclassificados ou inabilitados)



## 5.7. Tipo de Benefício



(código = 1) Participação exclusiva para ME/EPP

(código = 2) Subcontratação para ME/EPP

(código = 3) Cota reservada para ME/EPP

(código = 4) Sem benefício

(código = 5) Não se aplica



## 5.8. Situação do Resultado do Item da Contratação



(código = 1) Informado: Que possui valor e fornecedor e marca oriundo do resultado da contratação. Situação atribuída na inclusão do resultado do item da contratação.

(código = 2) Cancelado: Resultado do item cancelado conforme justificativa.



## 5.9. Tipo de Contrato



(código = 1) Contrato (termo inicial): Acordo formal recíproco de vontades firmado entre as partes

(código = 2) Comodato: Contrato de concessão de uso gratuito de bem móvel ou imóvel

(código = 3) Arrendamento: Contrato de cessão de um bem por um determinado período mediante pagamento

(código = 4) Concessão: Contrato firmado com empresa privada para execução de serviço público sendo remunerada por tarifa

(código = 5) Termo de Adesão: Contrato em que uma das partes estipula todas as cláusulas sem a outra parte poder modificá-las

(código = 6) Convênio: Acordos firmados entre as partes buscando a realização de um objetivo em comum

(código = 7) Empenho: É uma promessa de pagamento por parte do Estado para um fim específico

(código = 8) Outros: Outros tipos de contratos que não os listados

(código = 9) Termo de Execução Descentralizada (TED): Instrumento utilizado para a descentralização de crédito entre órgãos/entidades da União

(código = 10) Acordo de Cooperação Técnica (ACT): Acordos firmados entre órgãos visando a execução de programas de trabalho ou projetos

(código = 11) Termo de Compromisso: Acordo firmado para cumprir compromisso estabelecido entre as partes

(código = 12) Carta Contrato: Documento que formaliza e ratifica acordo entre duas ou mais partes nas hipóteses em que a lei dispensa a celebração de um contrato



## 5.10. Tipo de Termo de Contrato



(código = 1) Termo de Rescisão: Encerramento é antes da data final do contrato.

(código = 2) Termo Aditivo: Atualiza o contrato como um todo, podendo prorrogar, reajustar, acrescer, suprimir, alterar cláusulas e reajustar.

(código = 3) Termo de Apostilamento: Atualiza o valor do contrato.



## 5.11. Categoria do Processo



(código = 1) Cessão

(código = 2) Compras

(código = 3) Informática (TIC)

(código = 4) Internacional

(código = 5) Locação Imóveis

(código = 6) Mão de Obra

(código = 7) Obras

(código = 8) Serviços

(código = 9) Serviços de Engenharia

(código = 10) Serviços de Saúde

(código = 11) Alienação de bens móveis/imóveis



## 5.12. Tipo de Documento



Tipos de documentos da contratação:

(código = 1) Aviso de Contratação Direta

(código = 2) Edital

Outros anexos:

(código = 3) Minuta do Contrato

(código = 4) Termo de Referência

(código = 5) Anteprojeto

(código = 6) Projeto Básico

(código = 7) Estudo Técnico Preliminar

(código = 8) Projeto Executivo

(código = 9) Mapa de Riscos

(código = 10) DFD



Tipos de documentos da ata de registro de preço:

(código = 11) Ata de Registro de Preço



Tipos de documentos de contrato:

(código = 12) Contrato

(código = 13) Termo de Rescisão

(código = 14) Termo Aditivo

(código = 15) Termo de Apostilamento

(código = 17) Nota de Empenho

(código = 18) Relatório Final de Contrato



** Para outros documentos do processo usar o código 16.



## 5.13. Natureza Jurídica

# 

Código - Natureza jurídica 



0000 - Natureza Jurídica não informada

1015 - Órgão Público do Poder Executivo Federal

1023 - Órgão Público do Poder Executivo Estadual ou do Distrito Federal

1031 - Órgão Público do Poder Executivo Municipal

1040 - Órgão Público do Poder Legislativo Federal

1058 - Órgão Público do Poder Legislativo Estadual ou do Distrito Federal

1066 - Órgão Público do Poder Legislativo Municipal

1074 - Órgão Público do Poder Judiciário Federal

1082 - Órgão Público do Poder Judiciário Estadual

1104 - Autarquia Federal

1112 - Autarquia Estadual ou do Distrito Federal

1120 - Autarquia Municipal

1139 - Fundação Pública de Direito Público Federal

1147 - Fundação Pública de Direito Público Estadual ou do Distrito Federal

1155 - Fundação Pública de Direito Público Municipal

1163 - Órgão Público Autônomo Federal

1171 - Órgão Público Autônomo Estadual ou do Distrito Federal

1180 - Órgão Público Autônomo Municipal

1198 - Comissão Polinacional

1210 - Consórcio Público de Direito Público (Associação Pública)

1228 - Consórcio Público de Direito Privado

1236 - Estado ou Distrito Federal

1244 - Município

1252 - Fundação Pública de Direito Privado Federal

1260 - Fundação Pública de Direito Privado Estadual ou do Distrito Federal

1279 - Fundação Pública de Direito Privado Municipal

1287 - Fundo Público da Administração Indireta Federal

1295 - Fundo Público da Administração Indireta Estadual ou do Distrito Federal

1309 - Fundo Público da Administração Indireta Municipal

1317 - Fundo Público da Administração Direta Federal

1325 - Fundo Público da Administração Direta Estadual ou do Distrito Federal

1333 - Fundo Público da Administração Direta Municipal

1341 - União

2011 - Empresa Pública

2038 - Sociedade de Economia Mista

2046 - Sociedade Anônima Aberta

2054 - Sociedade Anônima Fechada

2062 - Sociedade Empresária Limitada

2070 - Sociedade Empresária em Nome Coletivo

2089 - Sociedade Empresária em Comandita Simples

2097 - Sociedade Empresária em Comandita por Ações

2100 - Sociedade Mercantil de Capital e Indústria

2127 - Sociedade em Conta de Participação

2135 - Empresário (Individual)

2143 - Cooperativa

2151 - Consórcio de Sociedades

2160 - Grupo de Sociedades

2178 - Estabelecimento, no Brasil, de Sociedade Estrangeira

2194 - Estabelecimento, no Brasil, de Empresa Binacional Argentino-Brasileira

2216 - Empresa Domiciliada no Exterior

2224 - Clube/Fundo de Investimento

2232 - Sociedade Simples Pura

2240 - Sociedade Simples Limitada

2259 - Sociedade Simples em Nome Coletivo

2267 - Sociedade Simples em Comandita Simples

2275 - Empresa Binacional

2283 - Consórcio de Empregadores

2291 - Consórcio Simples

2305 - Empresa Individual de Responsabilidade Limitada (de Natureza Empresária)

2313 - Empresa Individual de Responsabilidade Limitada (de Natureza Simples)

2321 - Sociedade Unipessoal de Advocacia

2330 - Cooperativas de Consumo

2348 - Empresa Simples de Inovação - Inova Simples

2356 - Investidor Não Residente

3034 - Serviço Notarial e Registral (Cartório)

3069 - Fundação Privada

3077 - Serviço Social Autônomo

3085 - Condomínio Edilício

3107 - Comissão de Conciliação Prévia

3115 - Entidade de Mediação e Arbitragem

3131 - Entidade Sindical

3204 - Estabelecimento, no Brasil, de Fundação ou Associação Estrangeiras

3212 - Fundação ou Associação Domiciliada no Exterior

3220 - Organização Religiosa

3239 - Comunidade Indígena

3247 - Fundo Privado

3255 - Órgão de Direção Nacional de Partido Político

3263 - Órgão de Direção Regional de Partido Político

3271 - Órgão de Direção Local de Partido Político

3280 - Comitê Financeiro de Partido Político

3298 - Frente Plebiscitária ou Referendária

3301 - Organização Social (OS)

3328 - Plano de Benefícios de Previdência Complementar Fechada

3999 - Associação Privada

4014 - Empresa Individual Imobiliária

4090 - Candidato a Cargo Político Eletivo

4120 - Produtor Rural (Pessoa Física)

5010 - Organização Internacional

5029 - Representação Diplomática Estrangeira

5037 - Outras Instituições Extraterritoriais

8885 - Natureza Jurídica não informada



## 5.14. Porte da Empresa



(código = 1) ME: Microempresa

(código = 2) EPP: Empresa de pequeno porte

(código = 3) Demais: Demais empresas

(código = 4) Não se aplica: Quando o fornecedor/arrematante for pessoa física.

(código = 5) Não informado: Quando não possuir o porte da empresa.



## 5.15. Amparo Legal



(código = 1) Lei 14.133/2021, Art. 28, I

(código = 2) Lei 14.133/2021, Art. 28, II  

(código = 3) Lei 14.133/2021, Art. 28, III 

(código = 4) Lei 14.133/2021, Art. 28, IV 

(código = 5) Lei 14.133/2021, Art. 28, V 

(código = 6) Lei 14.133/2021, Art. 74, I 

(código = 7) Lei 14.133/2021, Art. 74, II 

(código = 8) Lei 14.133/2021, Art. 74, III, a 

(código = 9) Lei 14.133/2021, Art. 74, III, b 

(código = 10) Lei 14.133/2021, Art. 74, III, c 

(código = 11) Lei 14.133/2021, Art. 74, III, d 

(código = 12) Lei 14.133/2021, Art. 74, III, e 

(código = 13) Lei 14.133/2021, Art. 74, III, f 

(código = 14) Lei 14.133/2021, Art. 74, III, g 

(código = 15) Lei 14.133/2021, Art. 74, III, h 

(código = 16) Lei 14.133/2021, Art. 74, IV 

(código = 17) Lei 14.133/2021, Art. 74, V 

(código = 18) Lei 14.133/2021, Art. 75, I 

(código = 19) Lei 14.133/2021, Art. 75, II 

(código = 20) Lei 14.133/2021, Art. 75, III, a 

(código = 21) Lei 14.133/2021, Art. 75, III, b 

(código = 22) Lei 14.133/2021, Art. 75, IV, a 

(código = 23) Lei 14.133/2021, Art. 75, IV, b 

(código = 24) Lei 14.133/2021, Art. 75, IV, c 

(código = 25) Lei 14.133/2021, Art. 75, IV, d 

(código = 26) Lei 14.133/2021, Art. 75, IV, e 

(código = 27) Lei 14.133/2021, Art. 75, IV, f 

(código = 28) Lei 14.133/2021, Art. 75, IV, g 

(código = 29) Lei 14.133/2021, Art. 75, IV, h 

(código = 30) Lei 14.133/2021, Art. 75, IV, i 

(código = 31) Lei 14.133/2021, Art. 75, IV, j 

(código = 32) Lei 14.133/2021, Art. 75, IV, k 

(código = 33) Lei 14.133/2021, Art. 75, IV, l 

(código = 34) Lei 14.133/2021, Art. 75, IV, m 

(código = 35) Lei 14.133/2021, Art. 75, V 

(código = 36) Lei 14.133/2021, Art. 75, VI 

(código = 37) Lei 14.133/2021, Art. 75, VII 

(código = 38) Lei 14.133/2021, Art. 75, VIII 

(código = 39) Lei 14.133/2021, Art. 75, IX 

(código = 40) Lei 14.133/2021, Art. 75, X 

(código = 41) Lei 14.133/2021, Art. 75, XI 

(código = 42) Lei 14.133/2021, Art. 75, XII 

(código = 43) Lei 14.133/2021, Art. 75, XIII 

(código = 44) Lei 14.133/2021, Art. 75, XIV 

(código = 45) Lei 14.133/2021, Art. 75, XV 

(código = 46) Lei 14.133/2021, Art. 75, XVI 

(código = 47) Lei 14.133/2021, Art. 78, I 

(código = 48) Lei 14.133/2021, Art. 78, II 

(código = 49) Lei 14.133/2021, Art. 78, III 

(código = 50) Lei 14.133/2021, Art. 74, caput

(Código = 51) Lei 14.284/2021, Art. 29, caput

(Código = 52) Lei 14.284/2021, Art. 24 § 1º

(Código = 53) Lei 14.284/2021, Art. 25 § 1º

(Código = 54) Lei 14.284/2021, Art. 34

(Código = 55) Lei 9.636/1998, Art. 11-C, I

(Código = 56) Lei 9.636/1998, Art. 11-C, II

(Código = 57) Lei 9.636/1998, Art. 24-C, I

(Código = 58) Lei 9.636/1998, Art. 24-C, II

(Código = 59) Lei 9.636/1998, Art. 24-C, III

(Código = 60) Lei 14.133/2021, Art. 75, XVII

(Código = 61) Lei 14.133/2021, Art. 76, I, a

(Código = 62) Lei 14.133/2021, Art. 76, I, b

(Código = 63) Lei 14.133/2021, Art. 76, I, c

(Código = 64) Lei 14.133/2021, Art. 76, I, d

(Código = 65) Lei 14.133/2021, Art. 76, I, e

(Código = 66) Lei 14.133/2021, Art. 76, I, f

(Código = 67) Lei 14.133/2021, Art. 76, I, g

(Código = 68) Lei 14.133/2021, Art. 76, I, h

(Código = 69) Lei 14.133/2021, Art. 76, I, i

(Código = 70) Lei 14.133/2021, Art. 76, I, j

(Código = 71) Lei 14.133/2021, Art. 76, II, a

(Código = 72) Lei 14.133/2021, Art. 76, II, b

(Código = 73) Lei 14.133/2021, Art. 76, II, c

(Código = 74) Lei 14.133/2021, Art. 76, II, d

(Código = 75) Lei 14.133/2021, Art. 76, II, e

(Código = 76) Lei 14.133/2021, Art. 76, II, f

(Código = 77) Lei 14.133/2021, Art. 75, XVIII

(Código = 78) Lei 14.628/2023, Art. 4º

(Código = 79) Lei 14.628/2023, Art. 12

(Código = 80) Lei 14.133/2021, Art. 1º, § 2º

## 

## 5.15. Categoria do Item do Plano de Contratações



(código = 1) Material

(código = 2) Serviço

(código = 3) Obras

(código = 4) Serviços de Engenharia

(código = 5) Soluções de TIC

(código = 6) Locação de Imóveis

(código = 7) Alienação/Concessão/Permissão

(código = 8) Obras e Serviços de Engenharia








# 6. Catálogo de Serviços (APIs)





## 6.1. Consultar Itens de PCA por Ano, idUsuario e Classificação Superior



Serviço que permite recuperar a lista de itens pertencentes a um determinado Plano de Contratações Anual (PCA) por determinado ano e usuário (Portais de Contratações), opcionalmente filtrando por ordem de classificação superior.

## 

### Detalhes de Requisição



### Dados de entrada

Nota: Alimentar o parâmetro {anoPca} e {idUsuario} na URL.



Nota: Dados a serem enviados no cabeçalho da requisição.



### Dados de retorno



### Códigos de Retorno





## 6.2. Consultar Itens de PCA por Ano e Classificação Superior



Serviço que permite recuperar a lista de itens pertencentes a um determinado Plano de Contratações Anual (PCA), opcionalmente filtrando por ordem de classificação superior.

## 

### Detalhes de Requisição



### Dados de entrada

Nota: Alimentar o parâmetro {ano} na URL.



Nota: Dados a serem enviados no cabeçalho da requisição.



### Dados de retorno



### Códigos de Retorno

## 

## 6.3. Serviço Consultar Contratações por Data de Publicação



Serviço que permite consultar contratações publicadas no PNCP por um período informado. Junto à data inicial e data final informadas deverá ser informado o código da Modalidade da Contratação (vide tabela  XXX). Opcionalmente poderá ser informado código do Modo de Disputa da Contratação (vide tabela  XXX), código do IBGE do Município, sigla da Unidade Federativa da Unidade Administrativa do Órgão, CNPJ do Órgão/Entidade, código da Unidade Administrativa do Órgão/Entidade ou código de identificação do Usuário (Sistema de Contratações Públicas que publicou a Contratação) para refinar a consulta.



### Detalhes de Requisição

## 

### Dados de entrada

Nota: Dados a serem enviados no cabeçalho da requisição.

### 

### Dados de retorno



### Códigos de Retorno







## 6.4. Serviço Consultar Contratações com Período de Recebimento de Propostas em Aberto



Serviço que permite consultar contratações publicadas no PNCP por um período informado. Opcionalmente poderá ser informado o código da Modalidade da Contratação (vide tabela  XXX), código do IBGE do Município, sigla da Unidade Federativa da Unidade Administrativa do Órgão, CNPJ do Órgão/Entidade, código da Unidade Administrativa do Órgão/Entidade ou código de identificação do Usuário (Sistema de Contratações Públicas que publicou a Contratação) para refinar a consulta.



### Detalhes de Requisição

## 

### Dados de entrada

Nota: Dados a serem enviados no cabeçalho da requisição.



### Dados de retorno



### Códigos de Retorno



6.4.1 - Observação:

Em adição ao serviço "6.4. Serviço Consultar Contratações com Período de Recebimento de Propostas em Aberto" mencionado neste manual, é importante destacar que o Portal Nacional de Contratações Públicas (PNCP) oferece uma gama ampla de funcionalidades via API que permitem uma consulta detalhada sobre CONTRATAÇÕES. Estas funcionalidades estão minuciosamente descritas no Manual de Integração — Portal Nacional de Contratações Públicas - PNCP, disponível no site oficial . Abaixo, apresentamos uma lista com alguns exemplos de serviços disponíveis:

6.3.5. Consultar uma Contratação

6.3.8. Consultar Todos Documentos de uma Contratação

6.3.9. Baixar Documento de uma Contratação

6.3.13. Consultar Itens de uma Contratação

6.3.14. Consultar Item de uma Contratação

6.3.17. Consultar Resultados de Item de uma Contratação

6.3.18. Consultar um Resultado específico de Item de uma Contratação

6.3.19. Consultar Histórico da Contratação

6.3.22. Consultar Imagens de um Item de Contratação



Recomendamos a leitura detalhada do Manual de Integração do PNCP para uma compreensão abrangente de todas as funcionalidades e possibilidades oferecidas pela API.

## 

## 6.5. Serviço Consultar Atas de Registro de Preço por Período de Vigência



Serviço que permite consultar atas de registro de preços publicadas no PNCP por um período informado. 

A partir da data inicial e data final informadas, serão recuperadas as atas cujo período de vigência coincida com o período informado. Opcionalmente poderá ser informado CNPJ do Órgão/Entidade, código da Unidade Administrativa do Órgão/Entidade ou número de identificação do Usuário (Portais de Contratações Públicas).



### Detalhes da Requisição



### Dados de entrada

Nota: Dados a serem enviados no cabeçalho da requisição.



### Dados de retorno



### Códigos de Retorno







6.5.1 - Observação:

Em adição ao serviço "6.5. Serviço Consultar Atas de Registro de Preço por Período de Vigência " mencionado neste manual, é importante destacar que o Portal Nacional de Contratações Públicas (PNCP) oferece uma gama ampla de funcionalidades via API que permitem uma consulta detalhada sobre CONTRATAÇÕES. Estas funcionalidades estão minuciosamente descritas no Manual de Integração — Portal Nacional de Contratações Públicas - PNCP, disponível no site oficial . Abaixo, apresentamos uma lista com alguns exemplos de serviços disponíveis:

6.4.4. Consultar Atas de Registro de Preço por Compra

6.4.8. Consultar Todos os Documentos de uma Ata 

6.4.9. Consultar Documento de uma Ata



Recomendamos a leitura detalhada do Manual de Integração do PNCP para uma compreensão abrangente de todas as funcionalidades e possibilidades oferecidas pela API.







## 6.6. Serviço Consultar Contratos por Data de Publicação



Serviço que permite consultar contratos e/ou empenhos com força de contrato publicados no PNCP por um período informado. A partir da data inicial e data final informadas serão recuperados os contratos/empenhos publicados no período. Opcionalmente poderá ser informado CNPJ do Órgão/Entidade, código da Unidade Administrativa do Órgão/Entidade ou número de identificação do Usuário (Portais de Contratações Públicas).

## 

### Detalhes de Requisição



### Dados de entrada

Nota: Dados a serem enviados no cabeçalho da requisição.



### Dados de retorno

### 

### Códigos de Retorno







# 


6.6.1 - Observação:

Em adição ao serviço "6.6. Serviço Consultar Contratos por Data de Publicação" mencionado neste manual, é importante destacar que o Portal Nacional de Contratações Públicas (PNCP) oferece uma gama ampla de funcionalidades via API que permitem uma consulta detalhada sobre CONTRATAÇÕES. Estas funcionalidades estão minuciosamente descritas no Manual de Integração — Portal Nacional de Contratações Públicas - PNCP, disponível no site oficial . Abaixo, apresentamos uma lista com alguns exemplos de serviços disponíveis:

6.5.7. Consultar Documento de um Contrato  

6.5.9. Consultar Contratos de uma Contratação



Recomendamos a leitura detalhada do Manual de Integração do PNCP para uma compreensão abrangente de todas as funcionalidades e possibilidades oferecidas pela API.







# 7. Suporte



Em caso de problemas durante o processo de integração do seu sistema com o PNCP, por favor entre em contato com a Central de Atendimento do Ministério da Gestão e da Inovação em Serviços Públicos () ou pelo telefone 0800 978 9001.



# 8. Glossário

O seguinte glossário fornece definições e explicações de termos e siglas específicos utilizados ao longo deste documento. O objetivo é esclarecer qualquer ambiguidade e ajudar o leitor a compreender melhor o conteúdo apresentado.



API (Application Programming Interface): Interface de Programação de Aplicações. É um conjunto de rotinas e padrões estabelecidos por um software para a utilização das suas funcionalidades por programas que não pretendem envolver-se em detalhes da implementação do software, mas apenas usá-lo.

CNBS (Catálogo Nacional de Bens e Serviços): Catálogo que lista e categoriza bens e serviços. Em muitos contextos, serve como uma referência padronizada para a classificação e descrição de itens. Mais informações em:  

CNPJ (Cadastro Nacional da Pessoa Jurídica): É o registro de empresas e outras entidades na Receita Federal do Brasil.

HTTP (Hypertext Transfer Protocol): Protocolo de Transferência de Hipertexto. É o protocolo fundamental da web, usado para transferir e exibir páginas da web, entre outros.

JSON (JavaScript Object Notation): Notação de Objeto JavaScript. É um formato de intercâmbio de dados leve e de fácil leitura e escrita para seres humanos.

ME/EPP: Microempresa e Empresa de Pequeno Porte. São categorias de empresas definidas pela legislação brasileira com base em seu faturamento.

PDM (Padrão Descritivo de Material): Refere-se a um padrão ou modelo utilizado para descrever materiais de forma consistente e padronizada, facilitando a identificação, catalogação e gestão de materiais em diversos sistemas e contextos.

PCA: plano de contratações anual definido na lei 14.133/2021

PNCP (Portal Nacional de Contratações Públicas): sítio oficial estabelecido pela Lei 14133 para divulgação e gestão de contratações públicas no Brasil. Centraliza informações, editais e contratos, promovendo transparência e eficiência, e é gerido por um comitê nacional.

REST (Representational State Transfer): Transferência de Estado Representacional. É um estilo arquitetural para desenvolvimento de serviços web. É caracterizado por um conjunto de restrições, incluindo um protocolo cliente/servidor sem estado e um conjunto padrão de métodos HTTP.

SWAGGER: É uma ferramenta de software de código aberto usada para projetar, construir e documentar serviços web REST.

TIC (Tecnologia da Informação e Comunicação): Refere-se a qualquer tecnologia que ajuda a produzir, manipular, armazenar, comunicar ou disseminar informação.

URL (Uniform Resource Locator): Localizador Padrão de Recursos. É um endereço de um recurso na web.

USUÁRIO: Em contextos de sistemas e aplicações, refere-se à pessoa ou entidade que utiliza o software ou sistema em questão.

${BASE_URL}: (a definir)

