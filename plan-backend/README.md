# Passo a passo para fluxo do backend para feature importação de dados em lote

## Ambiente de Desenvolvimento

```
  Para o desenvolvimento desta nova feature importação em lotes utilizaremos
  IBM Cloud Functions (baseado no Apache OpenWhisk) é uma plataforma Function-as-a-Service(FaaS)
  que executa funções em resposta a eventos recebidos.
```

**1-Desenvolver classe Data que recebara os dados brutos vindos do front**

```
/**
 * Class responsavel pela manipulação de Data
 * @param {String} [_id]
 * @class Data
 */
class Data {
    constructor() {

}
```

**2-Desenvolver método public import que sera responsável pela importação do arquivo juntamente com comapanyId,accountingId e date**

```

 /**
     * @public
     *Metodo responsâvel por realizar importação dos arquivo
     * @param {Object} data
     *  {String} data.accountingId
     *  {String} data.companyId
     *  {String} data.document Tipo de documento importado. Pode ser IncomeStatement ou BalanceSheet
     *  {String} data.date Data do document. Se for IncomeStatement precisa estar no inicio do ano. Se for Balancete, deve estar no início de cada mes (Data formatada)
     */

     import(data){
     // Validações que serão feitas no object
     }

```

**3-Criar repositorio com as funções que serão criadas no cloud functions**

```
Para criar o repositório, entramos no bitbucket e criamos o repositório dentro do projeto nucontdev.

```

**4-Criar no painel do cloud function ou via cli as ações que serão utlizadas**

```
ibmcloud fn action create nomeAcao arquivoAcao.js --kind nodejs:8

```

**5-Criar no painel do cloud function ou via cli a API Gateway**

```
ibmcloud fn api create -n

```

**6- Dentro API Gateway criar os verbos HTTP GET,POST,DELETE, UPDATE**

```
swagger: '2.0'
info:
  version: '1.0'
  title: api-refiner
paths:
  /add:
    post:
      operationId: postAdd
      x-openwhisk:
        namespace: rafael.nucont@gmail.com_dev
        action: cloudfunc
        package: default
        url: 'https://openwhisk.ng.bluemix.net/api/v1/web/rafael.nucont@gmail.com_dev/default/cloudfunc.json'
        auth: 4c4f174a-972c-43db-b9dd-0656ce960e95
      responses:
        '200':
          description: A successful invocation response
      parameters:
        - name: body
          in: body
          description: Request body
          required: false
          schema:
            type: object
  /pessoas:
    get:
      operationId: getPessoas
      x-openwhisk:
        namespace: rafael.nucont@gmail.com_dev
        action: cloudfunc
        package: default
        url: 'https://openwhisk.ng.bluemix.net/api/v1/web/rafael.nucont@gmail.com_dev/default/cloudfunc.json'
        auth: 4c4f174a-972c-43db-b9dd-0656ce960e95
      responses:
        '200':
          description: A successful invocation response
schemes:
  - https
consumes:
  - application/json
produces:
  - application/json
x-ibm-configuration:
  assembly:
    execute:
      - operation-switch:
          case:
            - operations:
                - postAdd
              execute:
                - set-variable:
                    actions:
                      - set: message.headers.X-Require-Whisk-Auth
                        value: 4c4f174a-972c-43db-b9dd-0656ce960e95
                - invoke:
                    target-url: 'https://openwhisk.ng.bluemix.net/api/v1/web/rafael.nucont@gmail.com_dev/default/cloudfunc.json'
                    verb: keep
            - operations:
                - getPessoas
              execute:
                - set-variable:
                    actions:
                      - set: message.headers.X-Require-Whisk-Auth
                        value: 4c4f174a-972c-43db-b9dd-0656ce960e95
                - invoke:
                    target-url: 'https://openwhisk.ng.bluemix.net/api/v1/web/rafael.nucont@gmail.com_dev/default/cloudfunc.json'
                    verb: keep
          otherwise: []
          title: whisk-invoke
  cors:
    enabled: true
basePath: /gws/apigateway/api/ec37ea5058c36e625681a95db348ff7e3eae4b32788f6456072e5ffc4724c038/app
host: service.us.apiconnect.ibmcloud.com
```

# Authors

-   **Rafael Lopes Fonseca** \- backend developer \- [RafaBarros93](https://github.com/RafaBarros93/)

# Thanks for

-   **Team NuHackers**
