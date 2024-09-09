
# PokeDIO - Pokémon Battle Smart Contract

![PokeDIO](https://ipfs.io/ipfs/QmaH6rupaTYFRYjtSFuqbfn2gn2gr4QFLSsE8T78qLquHf?filename=rambomon.png) <!-- Altere o link para uma imagem representativa do projeto -->

## Descrição

PokeDIO é um contrato inteligente em Solidity que simula batalhas entre Pokémons no blockchain. Ele permite que os jogadores criem, batalhem e curem seus Pokémons. O contrato utiliza o padrão ERC-721, o que significa que cada Pokémon é um token não fungível (NFT), garantindo a propriedade única e verificável dos Pokémons.

Este projeto foi desenvolvido utilizando a linguagem Solidity e a biblioteca OpenZeppelin para garantir segurança e conformidade com os padrões da Ethereum.

## Funcionalidades

- **Criação de Novos Pokémons**: O proprietário do jogo (gameOwner) pode criar novos Pokémons e atribuí-los a um jogador.
- **Batalha de Pokémons**: Proprietários de Pokémons podem realizar batalhas entre seus Pokémons e os de outros jogadores. Os Pokémons ganham níveis após as batalhas.
- **Sistema de Cura**: Proprietários podem curar seus Pokémons pagando uma pequena taxa em ether. A vida dos Pokémons será restaurada para o máximo após o pagamento.
- **Retirada de Fundos**: O proprietário do jogo pode retirar os fundos gerados pelo sistema de cura.

## Requisitos

- Solidity ^0.8.0
- OpenZeppelin Contracts (ERC-721)
- Node.js e npm para desenvolvimento e testes
- Ganache ou outra ferramenta de simulação de blockchain para testes locais
- MetaMask ou outro provedor de carteira Ethereum para interagir com o contrato

## Estrutura do Contrato

### `Pokemon` Struct

Cada Pokémon possui as seguintes propriedades:

- **name**: Nome do Pokémon.
- **level**: Nível do Pokémon (começa no nível 1 e aumenta conforme as batalhas).
- **img**: URL da imagem do Pokémon.
- **health**: Vida do Pokémon (começa com o máximo de 10 e diminui conforme as batalhas).

### Funções Principais

#### 1. `createNewPokemon(string memory _name, address _to, string memory _img)`

- Cria um novo Pokémon e o atribui a um jogador.
- Somente o proprietário do jogo (`gameOwner`) pode criar novos Pokémons.
- O novo Pokémon começa no nível 1 com a vida completa (10).
  
```solidity
function createNewPokemon(string memory _name, address _to, string memory _img) public;
```

#### 2. `battle(uint _attackingPokemon, uint _defendingPokemon)`

- Inicia uma batalha entre dois Pokémons.
- Somente o dono do Pokémon atacante pode iniciar a batalha.
- Se o atacante tiver nível maior ou igual ao defensor, o atacante ganha mais pontos de nível, mas ambos os Pokémons perdem vida.

```solidity
function battle(uint _attackingPokemon, uint _defendingPokemon) public;
```

#### 3. `healPokemon(uint _pokemonId)`

- Permite que o proprietário de um Pokémon pague uma taxa em ether para curar seu Pokémon.
- O custo da cura é `0.01 ether`.
- A vida do Pokémon é restaurada para o valor máximo (10).

```solidity
function healPokemon(uint _pokemonId) public payable;
```

#### 4. `withdraw()`

- Permite que o proprietário do jogo retire todos os fundos acumulados das curas pagas.
  
```solidity
function withdraw() public;
```

## Como Usar

### 1. Clone o Repositório

```bash
git clone https://github.com/usuario/pokedio.git
cd pokedio
```

### 2. Instale as Dependências

Instale as dependências necessárias, incluindo o OpenZeppelin, com:

```bash
npm install @openzeppelin/contracts
```

### 3. Compile o Contrato

Use o Hardhat, Truffle ou outra ferramenta de sua escolha para compilar o contrato:

```bash
npx hardhat compile
```

### 4. Deploy Localmente

Inicie uma blockchain local com o Ganache e faça o deploy do contrato. Exemplo com Hardhat:

```bash
npx hardhat node
npx hardhat run --network localhost scripts/deploy.js
```

### 5. Interação com o Contrato

Utilize ferramentas como Remix, Hardhat ou scripts Web3.js para interagir com o contrato. Certifique-se de ter saldo suficiente em ether para realizar as ações pagas, como curar Pokémons.

### 6. Teste o Contrato

Crie casos de teste para garantir que o contrato funcione corretamente. Exemplo com Hardhat:

```bash
npx hardhat test
```

## Contribuindo

Contribuições são bem-vindas! Se você deseja melhorar este contrato, siga as etapas abaixo:

1. Faça um fork deste repositório.
2. Crie uma branch para sua feature (`git checkout -b minha-feature`).
3. Faça commit das suas alterações (`git commit -m 'Adiciona nova feature'`).
4. Faça um push para a branch (`git push origin minha-feature`).
5. Abra um Pull Request.



---
