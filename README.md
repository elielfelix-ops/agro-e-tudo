# agro-e-tudo
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Minha Fazenda Interativa</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

    <div class="cenario">
        <div class="sol"></div>
        <div class="nuvem"></div>
        <div id="curral">
            </div>
        <div class="gramado"></div>
    </div>

    <div class="paineis-controle">
        <h2>Adicione animais à fazenda:</h2>
        <button onclick="adicionarAnimal('🐮')">Adicionar Vaca</button>
        <button onclick="adicionarAnimal('🐷')">Adicionar Porco</button>
        <button onclick="adicionarAnimal('🐔')">Adicionar Galinha</button>
        <button onclick="limparFazenda()" class="btn-limpar">Limpar Fazenda</button>
    </div>

    <script src="script.js"></script>
</body>
</html>
style.css
CSS
// Array para armazenar os itens do carrinho
let carrinho = [];
let total = 0;

// Função para adicionar produtos ao carrinho
function adicionarAoCarrinho(nomeProduto, precoProduto) {
    // Adiciona o produto ao array
    carrinho.push({ nome: nomeProduto, preco: precoProduto });
    
    // Atualiza o valor total
    total += precoProduto;
    
    // Atualiza a interface do site
    atualizarInterfaceCarrinho();
}

// Função para atualizar o HTML do carrinho
function atualizarInterfaceCarrinho() {
    const listaCarrinho = document.getElementById('lista-carrinho');
    const totalCarrinho = document.getElementById('total-carrinho');
    const contadorItens = document.getElementById('contador-itens');
    
    // Limpa a lista antes de reconstruir
    listaCarrinho.innerHTML = '';
    
    // Lista cada produto no carrinho
    carrinho.forEach((produto) => {
        const item = document.createElement('li');
        item.textContent = `${produto.nome} - R$ ${produto.preco.toFixed(2)}`;
        listaCarrinho.appendChild(item);
    });
    
    // Atualiza o texto do total e a quantidade de itens
    totalCarrinho.textContent = total.toFixed(2);
    contadorItens.textContent = carrinho.length;
}

// Função para enviar o pedido direto para o WhatsApp da loja
function finalizarPedido() {
    if (carrinho.length === 0) {
        alert("Seu carrinho está vazio! Adicione sementes ou insumos primeiro.");
        return;
    }
    
    // Cria o texto da mensagem
    let mensagem = "Olá, Sementes do Futuro! Gostaria de fazer o seguinte pedido:\n\n";
    
    carrinho.forEach((produto) => {
        mensagem += `- ${produto.nome}: R$ ${produto.preco.toFixed(2)}\n`;
    });
    
    mensagem += `\n*Total: R$ ${total.toFixed(2)}*`;
    
    // Codifica o texto para o formato de URL
    const mensagemCodificada = encodeURIComponent(mensagem);
    
    // Número fictício de WhatsApp da loja (substitua pelo real)
    const numeroWhats = "5511999999999"; 
    
    // Abre o WhatsApp com a mensagem pronta
    window.open(`https://wa.me/${numeroWhats}?text=${mensagemCodificada}`, '_blank');

<button onclick="adicionarAoCarrinho('Sementes de Milho Híbrido', 180.00)">
    Adicionar ao Carrinho
</button>

<div class="carrinho-container">
    <h3>Seu Carrinho (<span id="contador-itens">0</span>)</h3>
    <ul id="lista-carrinho">
        </ul>
    <p>Total: R$ <span id="total-carrinho">0,00</span></p>
    <button onclick="finalizarPedido()">Finalizar via WhatsApp 🌾</button>
</div>

<script src="script.js"></script>

/* Configuração do corpo da página */
body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background-color: #f0f0f0;
    margin: 0;
    padding: 20px;
    display: flex;
    flex-direction: column;
    align-items: center;
}

/* O cenário da fazenda */
.cenario {
    position: relative;
    width: 600px;
    height: 400px;
    background-color: #87CEEB; /* Céu azul */
    border: 8px solid #8B4513; /* Cerca de madeira */
    border-radius: 15px;
    overflow: hidden;
    box-shadow: 0 8px 16px rgba(0,0,0,0.2);
}

/* Sol */
.sol {
    position: absolute;
    top: 20px;
    right: 40px;
    width: 60px;
    height: 60px;
    background-color: #FFD700;
    border-radius: 50%;
    box-shadow: 0 0 20px #FFD700;
}

/* Grama */
.gramado {
    position: absolute;
    bottom: 0;
    width: 100%;
    height: 150px;
    background-color: #4CAF50; /* Verde grama */
}

/* Área onde os animais se movem */
#curral {
    position: absolute;
    width: 100%;
    height: 100%;
    z-index: 10;
}

/* Estilo dos emojis dos animais */
.animal {
    position: absolute;
    font-size: 40px;
    cursor: pointer;
    transition: transform 0.2s;
    user-select: none;
}

.animal:hover {
    transform: scale(1.2);
}

/* Painel de Botões */
.paineis-controle {
    margin-top: 20px;
    text-align: center;
    background: white;
    padding: 15px 25px;
    border-radius: 10px;
    box-shadow: 0 4px 6px rgba(0,0,0,0.1);
}

button {
    font-size: 16px;
    padding: 10px 15px;
    margin: 5px;
    border: none;
    border-radius: 5px;
    background-color: #8B4513;
    color: white;
    cursor: pointer;
    font-weight: bold;
}

button:hover {
    background-color: #A0522D;
}

.btn-limpar {
    background-color: #d9534f;
}

.btn-limpar:hover {
    background-color: #c9302c;
}
script.js
JavaScript


// Função para adicionar um animal em uma posição aleatória da grama
function adicionarAnimal(emoji) {
    const curral = document.getElementById('curral');
    
    // Cria o elemento do animal
    const novoAnimal = document.createElement('div');
    novoAnimal.classList.add('animal');
    novoAnimal.innerText = emoji;
    
    // Define posições aleatórias dentro do limite do gramado
    // O gramado tem 150px de altura e começa no final do cenário (altura 400px)
    const larguraCenario = 550; // 600px - tamanho do animal
    const topoMinimo = 250;     // Onde a grama começa
    const topoMaximo = 350;     // Perto do limite de baixo
    
    const posX = Math.floor(Math.random() * larguraCenario);
    const posY = Math.floor(Math.random() * (topoMaximo - topoMinimo)) + topoMinimo;
    
    novoAnimal.style.left = posX + 'px';
    novoAnimal.style.top = posY + 'px';
    
    // Faz o animal fazer um som (alerta simples) ou sumir ao ser clicado
    novoAnimal.onclick = function() {
        novoAnimal.style.transform = "scale(1.5)";
        setTimeout(() => {
            novoAnimal.remove(); // Remove o animal se você clicar nele
        }, 300);
    };
    
    // Adiciona o animal no cenário
    curral.appendChild(novoAnimal);
}

// Função para limpar todos os animais
function limparFazenda() {
    const curral = document.getElementById('curral');
    curral.innerHTML = '';
}
Como funciona:
HTML: Cria a estrutura da fazenda (div do cenário, céu, sol) e os botões de controle.

CSS: Deixa o cenário bonito, pinta o céu de azul, a grama de verde, e posiciona as coisas nos lugares certos usando position: absolute.

JavaScript: Quando você clica em um botão, o JS gera um novo elemento com o emoji do animal escolhido, calcula uma posição aleatória na grama para ele e o coloca na tela. Se você clicar no animal que está na grama, ele é "colhido" (desaparece).<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Minha Fazenda Interativa</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

    <div class="cenario">
        <div class="sol"></div>
        <div class="nuvem"></div>
        <div id="curral">
            </div>
        <div class="gramado"></div>
    </div>

    <div class="paineis-controle">
        <h2>Adicione animais à fazenda:</h2>
        <button onclick="adicionarAnimal('🐮')">Adicionar Vaca</button>
        <button onclick="adicionarAnimal('🐷')">Adicionar Porco</button>
        <button onclick="adicionarAnimal('🐔')">Adicionar Galinha</button>
        <button onclick="limparFazenda()" class="btn-limpar">Limpar Fazenda</button>
    </div>

    <script src="script.js"></script>
</body>
</html>
style.css
CSS


/* Configuração do corpo da página */
body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background-color: #f0f0f0;
    margin: 0;
    padding: 20px;
    display: flex;
    flex-direction: column;
    align-items: center;
}

/* O cenário da fazenda */
.cenario {
    position: relative;
    width: 600px;
    height: 400px;
    background-color: #87CEEB; /* Céu azul */
    border: 8px solid #8B4513; /* Cerca de madeira */
    border-radius: 15px;
    overflow: hidden;
    box-shadow: 0 8px 16px rgba(0,0,0,0.2);
}

/* Sol */
.sol {
    position: absolute;
    top: 20px;
    right: 40px;
    width: 60px;
    height: 60px;
    background-color: #FFD700;
    border-radius: 50%;
    box-shadow: 0 0 20px #FFD700;
}

/* Grama */
.gramado {
    position: absolute;
    bottom: 0;
    width: 100%;
    height: 150px;
    background-color: #4CAF50; /* Verde grama */
}

/* Área onde os animais se movem */
#curral {
    position: absolute;
    width: 100%;
    height: 100%;
    z-index: 10;
}

/* Estilo dos emojis dos animais */
.animal {
    position: absolute;
    font-size: 40px;
    cursor: pointer;
    transition: transform 0.2s;
    user-select: none;
}

.animal:hover {
    transform: scale(1.2);
}

/* Painel de Botões */
.paineis-controle {
    margin-top: 20px;
    text-align: center;
    background: white;
    padding: 15px 25px;
    border-radius: 10px;
    box-shadow: 0 4px 6px rgba(0,0,0,0.1);
}

button {
    font-size: 16px;
    padding: 10px 15px;
    margin: 5px;
    border: none;
    border-radius: 5px;
    background-color: #8B4513;
    color: white;
    cursor: pointer;
    font-weight: bold;
}

button:hover {
    background-color: #A0522D;
}

.btn-limpar {
    background-color: #d9534f;
}

.btn-limpar:hover {
    background-color: #c9302c;
}
script.js
JavaScript


// Função para adicionar um animal em uma posição aleatória da grama
function adicionarAnimal(emoji) {
    const curral = document.getElementById('curral');
    
    // Cria o elemento do animal
    const novoAnimal = document.createElement('div');
    novoAnimal.classList.add('animal');
    novoAnimal.innerText = emoji;
    
    // Define posições aleatórias dentro do limite do gramado
    // O gramado tem 150px de altura e começa no final do cenário (altura 400px)
    const larguraCenario = 550; // 600px - tamanho do animal
    const topoMinimo = 250;     // Onde a grama começa
    const topoMaximo = 350;     // Perto do limite de baixo
    
    const posX = Math.floor(Math.random() * larguraCenario);
    const posY = Math.floor(Math.random() * (topoMaximo - topoMinimo)) + topoMinimo;
    
    novoAnimal.style.left = posX + 'px';
    novoAnimal.style.top = posY + 'px';
    
    // Faz o animal fazer um som (alerta simples) ou sumir ao ser clicado
    novoAnimal.onclick = function() {
        novoAnimal.style.transform = "scale(1.5)";
        setTimeout(() => {
            novoAnimal.remove(); // Remove o animal se você clicar nele
        }, 300);
    };
    
    // Adiciona o animal no cenário
    curral.appendChild(novoAnimal);
}

// Função para limpar todos os animais
function limparFazenda() {
    const curral = document.getElementById('curral');
    curral.innerHTML = '';
}
Como funciona:
HTML: Cria a estrutura da fazenda (div do cenário, céu, sol) e os botões de controle.

CSS: Deixa o cenário bonito, pinta o céu de azul, a grama de verde, e posiciona as coisas nos lugares certos usando position: absolute.

JavaScript: Quando você clica em um botão, o JS gera um novo elemento com o emoji do animal escolhido, calcula uma posição aleatória na grama para ele e o coloca na tela. Se você clicar no animal que está na grama, ele é "colhido" (desaparece).
