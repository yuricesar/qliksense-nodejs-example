# qliksense-nodejs-example
Um exemplo de utilização backend NodeJs integrado ao Qlik Sense.

Pré-requisitos:

- Node.js
- Qlik Sense Server

Configuração:

- Node.js

i. Abrir cmd;
ii. Acessar diretório qliksense-nodejs-example do projeto;
iii. Instalar pacote executando "npm install" nesse diretório;
- Essa solução utiliza o pacote qlik-auth que está configurado como dependência do projeto;
iv. Abrir o arquivo index.html e atualizar o hostname e porta nas script tags na linha 6 para apontar pro seu qlik server;
v. Abrir script.js e configurar as variáveis appId e objectId para acessar seu ambiente de desenvolvimento;
- No link abaixo veja como obter appId e objectId;
- [Obtendo appId e objectId](https://help.qlik.com/en-US/sense-developer/February2020/Subsystems/Mashups/Content/Sense_Mashups/Howtos/mashups-obtain-app-object-id.htm)

- Qlik Sense Server

i. Abrir QMC (Qlik Management Console) e navegar até a área CONFIGURE SYSTEM > Virtual proxies;
ii. Crie um novo virtual proxy com um prefixo de sua escolha (você precisará desse prefixo ao configurar o Node.js)
iii. Na edição de virtual proxy, em Properties > Authentication, preencha o "Authentication module redirect URI" com http://node_server:3000/authenticate
- Porta 3000 está configurada em server.js e pode ser mudada como desejar
iv. Na edição de virtual proxy, em Properties > Advanced, adicione isto na seção "Additional response header": Access-Control-Allow-Origin:*
v. Novamente no QMC vá até CONFIGURE SYSTEM > Certficates
vi. Dê export no certificate, dando a ele o nome na máquina Node.js. Por padrão ficará salvo em C:\ProgramData\Qlik\Sense\Repository\Exported Certificates
vii. Copie o certificado client para a raíz do projeto Node.js
- No link abaixo tutorial de como exportar certificados
- [Exportando Certificados](https://support.qlik.com/articles/000005433)

Como funcona:

1. O arquivo script.js tenta carregar o qlik.js do Qlik Sense Server configurado;
2. Nesse ponto o 'Authentication module redirect URI' no proxy virtual é chamado;
3. Isso é solucionado pelo arquivo server.js e cria usuário hardcode chamado "sample";
4. O módulo qlik-auth é chamado para enviar um pedido de ticket com a configuração especificada;
5. Um ticketId é retornado e a sessão estabelecida;
6. Não é necessária nenhuma entrada por parte do usuário.
