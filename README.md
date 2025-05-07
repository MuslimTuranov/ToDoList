# Sample Hardhat Project

This project demonstrates a basic Hardhat use case. It comes with a sample contract, a test for that contract, and a Hardhat Ignition module that deploys that contract.

Try running some of the following tasks:

```shell
npx hardhat help
npx hardhat test
REPORT_GAS=true npx hardhat test
npx hardhat node
npx hardhat ignition deploy ./ignition/modules/Lock.js
```

# Децентрализованное ToDo-приложение

## Описание проекта

Это децентрализованное веб-приложение (dApp), позволяющее пользователю создавать, удалять и изменять статус задач. Все данные хранятся в блокчейне Ethereum (сеть Sepolia). Пользователь взаимодействует с контрактом через MetaMask и Web3.js.

Фронтенд написан на React, взаимодействие с блокчейном осуществляется через Web3.js и смарт-контракт, написанный на Solidity. Для подключения используется MetaMask, а для связи с блокчейном — Alchemy RPC.

## Функциональность

- Просмотр всех задач из смарт-контракта
- Добавление новых задач
- Отметка задачи как выполненной 
- Удаление задачи
- Подключение аккаунта MetaMask для выполнения транзакций

## Установка

### 1. Установка зависимостей

Для начала, необходимо установить следующие зависимости:

- **Node.js**: Для работы с React и Web3.js.
- **MetaMask**: Для подключения к блокчейну Ethereum.

После этого установите необходимые пакеты:

```shell
npm install react web3
```
2. Развертывание смарт-контракта
Напишите смарт-контракт TodoList.sol, как указано в коде.

Разверните контракт в сети Ethereum (например, Sepolia) с помощью Remix IDE или Hardhat.

Получите адрес контракта после развертывания.

3. Настройка Frontend
Создайте новый React проект или используйте существующий.

Установите и импортируйте Web3.js:

```shell
npm install web3
```
Добавьте код для взаимодействия с контрактом в вашем React приложении, используя контрактный адрес и ABI.

Пример кода подключения к смарт-контракту:

```shell
const contractAddress = "<contract-address>";
const contractABI = [...]; // Вставьте ABI контракта

const web3 = new Web3(window.ethereum);
const contract = new web3.eth.Contract(contractABI, contractAddress);
```
4. Подключение MetaMask
Добавьте кнопку для подключения к MetaMask:

```shell
const connectMetaMask = async () => {
  if (window.ethereum) {
    try {
      await window.ethereum.request({ method: 'eth_requestAccounts' });
      const accounts = await web3.eth.getAccounts();
      setAccount(accounts[0]);
    } catch (err) {
      console.error('Ошибка подключения MetaMask:', err);
    }
  } else {
    alert('Пожалуйста, установите MetaMask');
  }
};
```
5. Добавление и управление задачами
Для создания задачи используйте функцию createTask контракта:

```shell
const createTask = async () => {
  try {
    await contract.methods.createTask(taskDescription).send({ from: account });
    // Обновите список задач
  } catch (err) {
    console.error('Ошибка при создании задачи:', err);
  }
};
```
Для изменения статуса задачи:

```shell
const toggleCompleted = async (id) => {
  try {
    await contract.methods.toggleCompleted(id).send({ from: account });
    // Обновите статус задачи
  } catch (err) {
    console.error('Ошибка при изменении статуса задачи:', err);
  }
};
```
Для удаления задачи:

```shell
const deleteTask = async (id) => {
  try {
    await contract.methods.deleteTask(id).send({ from: account });
    // Удалите задачу из списка
  } catch (err) {
    console.error('Ошибка при удалении задачи:', err);
  }
};
```
6. Запуск приложения
Убедитесь, что MetaMask подключен и что у вас есть эфир на тестовой сети (например, Sepolia).

Запустите ваше React приложение:

```shell
npm start
```