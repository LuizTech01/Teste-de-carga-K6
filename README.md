# Testes de Performance com K6

Este repositório contém testes de performance utilizando a ferramenta [K6](https://k6.io/) para avaliar a API de demonstração disponível em [https://test-api.k6.io/](https://test-api.k6.io/).

## Requisitos

Antes de executar os testes, certifique-se de ter o K6 instalado:

- [K6](https://k6.io/docs/getting-started/installation/)

## Como Executar os Testes

Para rodar um teste de carga, utilize o seguinte comando:

```sh
k6 run nome-do-seu-teste.js
```

Caso queira especificar um teste com diferentes parâmetros de carga, utilize:

```sh
k6 run --vus 10 --duration 30s script.js
```

Isso significa que o teste será executado com 10 usuários virtuais por 30 segundos.


## Exemplo de Script K6

Aqui está um exemplo de script de teste:

```javascript
import http from 'k6/http';
import { check, sleep } from 'k6';

export let options = {
  vus: 10, // Número de usuários virtuais
  duration: '30s', // Duração do teste
};

export default function () {
  let res = http.get('https://test-api.k6.io/public/crocodiles/');
  check(res, {
    'status code is 200': (r) => r.status === 200,
  });
  sleep(1);
}
```

## Relatórios e Análise

Para visualizar um resumo dos resultados ao final da execução:

```sh
k6 run nome-do-seu-teste.js
```