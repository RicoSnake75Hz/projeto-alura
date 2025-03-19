let amigos = new Set();


// Evento para adicionar um amigo usando a tecla enter
document.getElementById("amigo").addEventListener("keypress", function(event) {
    if (event.key === "Enter") {  
        event.preventDefault();
        adicionarAmigo();
    }
});


/**
 * Adiciona um novo amigo na lista
 */
function adicionarAmigo() {
    const input = document.getElementById("amigo");
    const nome = input.value.trim();

    if (!nome) {
        alert("⚠️ O atenção esse campo não pode estar vazio!");
        return;
    }

    if (amigos.has(nome)) {
        alert("🔁 Esse amigo já está na lista!");
        return;
    }

    amigos.add(nome);
    input.value = ""; // Limpa o campo após adicionar
    atualizarLista();
}

/**
 * Atualiza a exibição da lista de amigos na tela
 */
function atualizarLista() {
    const lista = document.getElementById("listaAmigos");
    lista.innerHTML = "";

    
    Array.from(amigos).forEach((amigo) => {
        const li = document.createElement("li");
        li.textContent = amigo;

        const btnRemover = document.createElement("button");
        btnRemover.textContent = "🚮";
        btnRemover.classList.add("remove-button");

        // Adiciona evento para remover amigo
        btnRemover.onclick = () => removerAmigo(amigo);

        li.appendChild(btnRemover);
        lista.appendChild(li);
    });
}

/**
 * Remove o amigo da lista
 */
function removerAmigo(nome) {
    amigos.delete(nome);
    atualizarLista();
}

/**
 * Realiza o sorteio de um amigo secreto
 */
function sortearAmigo() {
    if (amigos.size === 0) {
        alert(`🚨 Alerta de Solidão Extrema 🚨
        Parece que sua lista de amigos está mais vazia que a geladeira de universitário no fim do mês. 🥲
        Adicione pelo menos um amigo para poder sortear.
        Se precisar, podemos abrir uma vaquinha para comprar você um amigo. 😂`);
        return; // Impede que o sorteio continue caso a lista esteja vazia, e exibe essa mensagem.
    }

    const amigosArray = Array.from(amigos); // Converte Set 
    const sorteadoIndex = Math.floor(Math.random() * amigosArray.length);
    const sorteado = amigosArray[sorteadoIndex];

    const resultado = document.getElementById("resultado");
    resultado.innerHTML = `<li>🫂 O amigo secreto é: <strong>${sorteado}</strong> 🎁</li>`;
}
