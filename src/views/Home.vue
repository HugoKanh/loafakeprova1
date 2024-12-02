<template>
  <div class="container mt-4">
    <!-- Barra de Navegação -->
    <nav class="mb-4 d-flex justify-content-end">
      <router-link to="/login" class="btn btn-primary">Login</router-link>
    </nav>

    <h1 class="text-center">
      Bem-vindo ao Fakeboard
      <img class="logo-inline ms-2" src="@/assets/imagens/Fake.png" alt="Fake" />
    </h1>

    <p class="mt-4 paragrafo-centralizado">
      Fakeboard: Sua Gestão em Um Só Lugar<br>

O Fakeboard é a solução ideal para quem busca centralizar informações e simplificar processos. <br>
Com uma interface intuitiva e bem organizada, o painel oferece uma visão abrangente e prática de todas as funcionalidades disponíveis no sistema.<br>
✔ Centralização e Controle:
Tenha todas as informações ao alcance de poucos cliques, desde dados detalhados até o gerenciamento completo de tarefas. Acompanhe métricas em tempo real, identifique prioridades e analise resultados com facilidade, garantindo uma visão clara e precisa do desempenho das operações.<br>

✔ Navegação Ágil:
Desenvolvido para uma experiência fluida, o Fakeboard permite alternar rapidamente entre diferentes áreas do sistema, otimizando seu tempo e esforço.<br>

✔ Decisões Mais Estratégicas:
Com ferramentas avançadas de gestão, você toma decisões mais rápidas e embasadas, direcionando esforços para o que realmente importa. A redução de tarefas manuais e a automação de processos proporcionam maior produtividade e foco nos objetivos.<br>

Fakeboard O Painel Que Transforma Sua Gestão:<br>
Mais que um dashboard, é sua porta de entrada para uma administração estratégica, integrada e eficaz. Simplifique operações e eleve sua performance ao próximo nível.
    </p>

    <!-- Redes Sociais -->
    <section class="redes-sociais text-center mt-5">
      <h2>Conecte-se Conosco</h2>
      <div class="d-flex justify-content-center gap-4 mt-3">
        <a href="https://www.instagram.com/" target="_blank">
          <img src="https://upload.wikimedia.org/wikipedia/commons/a/a5/Instagram_icon.png" alt="Instagram" width="50" />
        </a>
        <a href="https://www.facebook.com/" target="_blank">
          <img src="https://upload.wikimedia.org/wikipedia/commons/5/51/Facebook_f_logo_%282019%29.svg" alt="Facebook" width="50" />
        </a>
        <a href="https://www.linkedin.com/" target="_blank">
          <img src="https://upload.wikimedia.org/wikipedia/commons/e/e9/Linkedin_icon.svg" alt="LinkedIn" width="50" />
        </a>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: "Home",
};
</script>

<style>
/* Geral */
body {
  font-family: 'Arial', sans-serif;
  margin: 0;
  padding: 0;
  background-color: #f0f4f8; /* Azul claro para o fundo */
  color: #333; /* Preto para o texto */
}

.container {
  max-width: 1200px;
  margin: auto;
  padding: 20px;
}

/* Títulos */
h1, h2 {
  color: #002B5C; /* Azul escuro */
}

/* Barra de Navegação */
nav {
  background-color: #002B5C; /* Azul escuro */
  padding: 10px 20px;
  border-radius: 8px;
}

nav .btn {
  background-color: #007BFF; /* Azul padrão */
  color: #fff;
  border: none;
  border-radius: 5px;
  padding: 10px 20px;
  text-decoration: none;
  font-weight: bold;
}

nav .btn:hover {
  background-color: #0056b3; /* Azul escuro no hover */
}

/* Logo Inline */
.logo-inline {
  width: 50px;
  vertical-align: middle;
}

/* Parágrafo */
p {
  font-size: 1.1rem;
  line-height: 1.6;
  color: #555; /* Cinza médio */
}

/* Redes Sociais */
.redes-sociais {
  margin-top: 40px;
}

.redes-sociais h2 {
  color: #002B5C; /* Azul escuro */
}

.redes-sociais a img {
  border-radius: 50%;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.redes-sociais a img:hover {
  transform: scale(1.1); /* Ampliação no hover */
  box-shadow: 0px 4px 10px rgba(0, 43, 92, 0.5); /* Sombra azul */
}
/* Estilo para o parágrafo centralizado */
.paragrafo-centralizado {
  text-align: center; /* Centraliza o texto */
  font-size: 1.2rem; /* Aumenta o tamanho da fonte */
  color: #002B5C; /* Azul escuro */
  background: linear-gradient(90deg, #007BFF, #002B5C); /* Fundo gradiente */
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent; /* Torna o texto gradiente */
  padding: 20px;
  border: 2px solid #007BFF; /* Borda azul */
  border-radius: 8px; /* Bordas arredondadas */
  box-shadow: 0px 4px 10px rgba(0, 43, 92, 0.2); /* Sombra leve */
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.paragrafo-centralizado:hover {
  transform: scale(1.05); /* Ampliação no hover */
  box-shadow: 0px 6px 15px rgba(0, 43, 92, 0.4); /* Sombra mais intensa no hover */
}


/* Responsividade */
@media (max-width: 768px) {
  h1 {
    font-size: 1.8rem;
  }

  p {
    font-size: 1rem;
  }

  .redes-sociais a img {
    width: 40px;
  }
}

</style>