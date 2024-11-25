carrinho.html
<!DOCTYPE html>
<html lang="pt-BR">

<head>
    <meta charset="UTF-8">
    <title>Carrinho de Compras</title>
    <link rel="icon" href="img/logo.png" type="image/png">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="style.css">
</head>

<body>
    <header>
        <nav class="navbar navbar-expand-lg fixed-top">
            <div class="container-fluid">
                <a class="navbar-brand mx-auto" href="index.html">
                    <img src="img/logo.png" alt="Logo Zona Street" width="130" height="50">
                </a>
                <div>
                    <a href="index.html" class="btn btn-secondary">Voltar à Loja</a>
                </div>
            </div>
        </nav>
    </header>

    <main class="container mt-5">
        <h1 class="text-center mb-4">Carrinho de Compras</h1>
        <div id="cart-items" class="row"></div>
        <div class="text-end mt-4">
            <h3>Total: <span id="cart-total">R$ 0,00</span></h3>
            <button class="btn btn-success" id="checkout-btn">Finalizar Compra</button>
        </div>
    </main>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
    <script>
        // Recupera os itens do carrinho do localStorage
        const cartItems = JSON.parse(localStorage.getItem('cart')) || [];
        const cartContainer = document.getElementById('cart-items');
        const cartTotal = document.getElementById('cart-total');

        function renderCart() {
            cartContainer.innerHTML = ''; // Limpa o conteúdo
            let total = 0;

            if (cartItems.length === 0) {
                cartContainer.innerHTML = '<p class="text-center">Seu carrinho está vazio.</p>';
            } else {
                cartItems.forEach((item, index) => {
                    const itemElement = document.createElement('div');
                    itemElement.classList.add('col-12', 'mb-3');

                    itemElement.innerHTML = `
                        <div class="card shadow-sm">
                            <div class="row g-0">
                                <div class="col-md-2">
                                    <img src="${item.image}" alt="${item.name}" class="img-fluid rounded-start">
                                </div>
                                <div class="col-md-8">
                                    <div class="card-body">
                                        <h5 class="card-title">${item.name}</h5>
                                        <p class="card-text">${item.price}</p>
                                    </div>
                                </div>
                                <div class="col-md-2 d-flex align-items-center justify-content-center">
                                    <button class="btn btn-danger remove-btn" data-index="${index}">Remover</button>
                                </div>
                            </div>
                        </div>
                    `;

                    cartContainer.appendChild(itemElement);

                    // Calcula o total
                    const price = parseFloat(item.price.replace('R$', '').replace(',', '.'));
                    total += price;
                });

                cartTotal.textContent = `R$ ${total.toFixed(2).replace('.', ',')}`;
            }
        }

        // Evento para remover item
        cartContainer.addEventListener('click', (e) => {
            if (e.target.classList.contains('remove-btn')) {
                const itemIndex = e.target.dataset.index;
                cartItems.splice(itemIndex, 1); // Remove o item do array
                localStorage.setItem('cart', JSON.stringify(cartItems)); // Atualiza o localStorage
                renderCart(); // Re-renderiza o carrinho
            }
        });

        // Finalizar compra
        document.getElementById('checkout-btn').addEventListener('click', () => {
            if (cartItems.length === 0) {
                alert('O carrinho está vazio. Adicione itens antes de finalizar a compra.');
            } else {
                alert('Compra finalizada com sucesso!');
                localStorage.removeItem('cart'); // Limpa o carrinho
                renderCart();
            }
        });

        // Renderiza o carrinho ao carregar a página
        renderCart();
    </script>
</body>

</html>




index.html
<!DOCTYPE html>
<html lang="pt-BR">

<head>
    <meta charset="UTF-8">
    <title>Zona Street</title>
    <link rel="icon" href="img/logo.png" type="image/png">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap-icons/font/bootstrap-icons.css" rel="stylesheet">
    <link rel="stylesheet" href="style.css">
</head>

<body>
    <header>
        <nav class="navbar navbar-expand-lg fixed-top">
            <div class="container-fluid">
                <a class="navbar-brand mx-auto" href="index.html">
                    <img src="img/logo.png" alt="Logo Zona Street" width="130" height="50">
                </a>
                <button class="navbar-toggler bg-dark" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent">
                    <span class="navbar-toggler-icon"></span>
                </button>
                <div class="collapse navbar-collapse" id="navbarSupportedContent">
                    <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                        <li class="nav-item">
                            <a class="nav-link" href="quemsomos.html"><strong>Quem somos</strong></a>
                        </li>
                        <li class="nav-item dropdown">
                            <a class="nav-link dropdown-toggle" href="#" role="button" data-bs-toggle="dropdown">
                                <strong>Produtos</strong>
                            </a>
                            <ul class="dropdown-menu">
                                <li><a class="dropdown-item" href="camisetas.html">Camisetas</a></li>
                                <li><a class="dropdown-item" href="calças.html">Calças</a></li>
                                <li>
                                    <hr class="dropdown-divider">
                                </li>
                                <li>
                                    <button type="button" class="dropdown-item" data-bs-toggle="modal" data-bs-target="#exampleModal">Fale conosco</button>
                                </li>
                            </ul>
                        </li>
                    </ul>
                    <!-- Ícone do Carrinho -->
                    <a href="carrinho.html" class="btn btn-outline-dark">
                        <span class="me-1">Carrinho</span>
                        <i class="bi bi-cart"></i>
                    </a>
                </div>
            </div>
        </nav>
    </header>

    <main>
        <div id="imagemd" class="imgdesc text-center">
            <img src="img/ZON41.png" alt="Imagem de Destaque Zona Street" class="img-fluid rounded">
        </div>
        <div class="lançamento">
            <p>
                <strong>LANÇAMENTOS</strong>
            </p>
        </div>

        <div class="container">
            <div class="row row-cols-1 row-cols-md-2 g-4 mt-4">

                <div class="col">
                    <div class="card shadow-sm">
                        <img src="img/CamisaTiger.png" alt="Camisa Zona Street Tiger" class="card-img-top img-fluid">
                        <div class="card-body">
                            <h5 class="card-title">Camisa Tiger</h5>
                            <p class="card-text">R$ 79,99</p>
                            <button class="btn btn-primary w-100 buy-btn">Comprar</button>
                        </div>
                    </div>
                </div>

                <div class="col">
                    <div class="card shadow-sm">
                        <img src="img/BonéZona.png" alt="Boné Zona Street" class="card-img-top img-fluid">
                        <div class="card-body">
                            <h5 class="card-title">Boné Zona Street</h5>
                            <p class="card-text">R$ 119,99</p>
                            <button class="btn btn-primary w-100 buy-btn">Comprar</button>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Modal Fale Conosco -->
            <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
                <div class="modal-dialog">
                    <div class="modal-content">
                        <div class="modal-header">
                            <h1 class="modal-title fs-5" id="exampleModalLabel">Fale conosco</h1>
                            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                        </div>
                        <div class="modal-body">
                            <form>
                                <div class="mb-3">
                                    <label for="nome" class="col-form-label">Nome: *</label>
                                    <input type="text" class="form-control" id="nome" required>
                                </div>
                                <div class="mb-3">
                                    <label for="email" class="col-form-label">E-mail: *</label>
                                    <input type="email" class="form-control" id="email" required>
                                </div>
                                <div class="mb-3">
                                    <label for="assunto" class="col-form-label">Assunto: *</label>
                                    <input type="text" class="form-control" id="assunto" required>
                                </div>
                                <div class="mb-3">
                                    <label for="mensagem" class="col-form-label">Mensagem: *</label>
                                    <textarea class="form-control" id="mensagem" rows="4" required></textarea>
                                </div>
                            </form>
                        </div>
                        <div class="modal-footer">
                            <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Fechar</button>
                            <button type="submit" class="btn btn-primary">Enviar</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </main>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>

    <script>
        const buyButtons = document.querySelectorAll('.buy-btn');
    
        buyButtons.forEach(button => {
            button.addEventListener('click', (e) => {
                e.preventDefault();
    
                // Encontre os detalhes do produto
                const card = button.closest('.card');
                const productName = card.querySelector('.card-title').textContent;
                const productPrice = card.querySelector('.card-text').textContent;
                const productImage = card.querySelector('img').src;
    
                // Crie o item do produto
                const product = {
                    name: productName,
                    price: productPrice,
                    image: productImage
                };
    
                // Adicione o produto ao localStorage
                let cart = JSON.parse(localStorage.getItem('cart')) || [];
                cart.push(product);
                localStorage.setItem('cart', JSON.stringify(cart));
    
                alert('Seu item foi adicionado ao carrinho!');
            });
        });
    
        // Exibir os itens do carrinho
        const viewCartButton = document.getElementById('view-cart');
        viewCartButton.addEventListener('click', () => {
            let cart = JSON.parse(localStorage.getItem('cart')) || [];
            if (cart.length === 0) {
                alert('O carrinho está vazio.');
            } else {
                let cartContent = 'Itens no carrinho:\n\n';
                cart.forEach((item, index) => {
                    cartContent += `${index + 1}. ${item.name} - ${item.price}\n`;
                });
                alert(cartContent);
            }
        });
    </script>
    

</body>

</html>
