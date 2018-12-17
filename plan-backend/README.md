# Passo a passo para fluxo do backend para feature importação de dados em lote

## Ambiente de Desenvolvimento

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

**3- Desenvolver a classe ou cloud function DocumentClassifier**

**4-Desenvolver a classe ou cloud function**

**5-**

# Authors

-   **Rafael Lopes Fonseca** \- backend developer \- [RafaBarros93](https://github.com/RafaBarros93/)

# Thanks for

-   **Team NuHackers**
