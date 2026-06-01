# Testes na API ViaCEP

## Cenário 1: CEP válido
- URL: https://viacep.com.br/ws/01001000/json/
- Status: 200
- Validações que faria:
  - O campo "cep" deve corresponder ao CEP consultado
  - O campo "logradouro" não pode estar vazio
  - O campo "uf" deve ter 2 letras maiúsculas

## Cenário 2: CEP inexistente
- URL: https://viacep.com.br/ws/99999999/json/
- Status: 200 (mas atenção: o JSON contém "erro": true)
- Validação: Deveria ser 404? Discutível. Reportaria como melhoria.
