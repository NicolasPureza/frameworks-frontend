# Aula 09 — Projeto React 02

**Disciplina:** Frameworks Front-end  
**Foco:** State e `useState`, Formulários controlados, `useEffect` (e limpeza), Consumo de APIs (`fetch` GET/POST) e React Router (`BrowserRouter`, `Routes`, `Route`, `Link`, `useParams`).  
**Professor:** Prof. Me. Deivison S. Takatu (`deivison.takatu@edu.senai.br`)

---

## 📌 Sumário

1. [State e `useState`](#1-state-e-usestate)
2. [Formulários Controlados](#2-formulários-controlados)
3. [`useEffect` e Limpeza de Efeitos](#3-useeffect-e-limpeza-de-efeitos)
4. [Consumo de APIs com `fetch`](#4-consumo-de-apis-com-fetch)
5. [React Router (`react-router-dom`)](#5-react-router-react-router-dom)
6. [Atividade Prática](#6-atividade-prática)
7. [Referências](#7-referências)

---

## 1. State e `useState`

* **State** é uma informação que o componente guarda entre renderizações (como um contador, uma mensagem ou uma lista).
* Variáveis comuns não disparam nova renderização da interface ao mudar de valor; já o `useState` retorna `[valorAtual, funcaoAtualizadora]` e informa ao React quando atualizar a tela.
* **Hooks** são funções especiais iniciadas com `use` e devem ser chamadas no nível superior do componente funcional.

```jsx
import { useState } from "react";

function Contador() {
  const [contador, setContador] = useState(0);

  return (
    <section>
      <p>Valor: {contador}</p>
      <button onClick={() => setContador(contador + 1)}>
        Incrementar
      </button>
    </section>
  );
}
```

---

## 2. Formulários Controlados

* Em React, **campos controlados** têm seu valor gerenciado pelo estado do componente:
  * `value={estado}` define o texto exibido no campo;
  * `onChange={(e) => setEstado(e.target.value)}` atualiza o estado a cada digitação.
* No envio do formulário (`onSubmit`), utiliza-se `e.preventDefault()` para evitar o recarregamento padrão da página pelo navegador, permitindo validar e tratar os dados diretamente no React.

```jsx
function Formulario() {
  const [nome, setNome] = useState("");

  function enviar(e) {
    e.preventDefault();
    alert(`Enviado: ${nome}`);
  }

  return (
    <form onSubmit={enviar}>
      <input value={nome} onChange={(e) => setNome(e.target.value)} />
      <button type="submit">Enviar</button>
    </form>
  );
}
```

---

## 3. `useEffect` e Limpeza de Efeitos

* **Efeitos** executam ações fora da renderização pura da interface, sincronizando o componente com sistemas externos (título da aba, temporizadores, eventos de janela, APIs).
* O segundo parâmetro do `useEffect` é o **array de dependências**:
  * `[]` executa apenas na montagem do componente;
  * `[titulo]` executa na montagem e sempre que `titulo` mudar.
* **Limpeza (cleanup):** retornar uma função dentro do `useEffect` cancela listeners, temporizadores ou requisições pendentes quando as dependências mudam ou o componente é desmontado.

```jsx
useEffect(() => {
  window.addEventListener("resize", atualizar);
  return () => {
    window.removeEventListener("resize", atualizar);
  };
}, []);
```

---

## 4. Consumo de APIs com `fetch`

* `fetch()` realiza requisições HTTP assíncronas (`GET`, `POST`, etc.) e `response.json()` converte o retorno JSON.
* Boas práticas essenciais:
  * Verificar `if (!response.ok) throw new Error(...)`;
  * Usar `try / catch` para tratar erros de rede e HTTP;
  * Tratar estados de **carregamento**, **erro** e **estado vazio** na interface;
  * Em requisições `POST`, informar `method: "POST"`, `headers: { "Content-Type": "application/json" }` e `body: JSON.stringify(...)`.

---

## 5. React Router (`react-router-dom`)

* Biblioteca para roteamento em SPAs (navegação entre telas sem recarregar todo o documento):
  * `BrowserRouter`: envolve a aplicação;
  * `Routes` e `Route`: associam caminhos (`path`) a componentes (`element`);
  * `Link`: navegação interna via propriedade `to`;
  * `useParams()`: lê parâmetros variáveis da URL (ex.: `/cursos/:id`) para páginas de detalhes.

```jsx
import { BrowserRouter, Routes, Route, Link, useParams } from "react-router-dom";

function Detalhes() {
  const { id } = useParams();
  return <h1>Item: {id}</h1>;
}
```

---

## 6. Atividade Prática

Desenvolver uma aplicação React que utilize **todos os conceitos estudados**:
- `State` e `useState`
- Formulários controlados
- `useEffect` (incluindo limpeza)
- Consumo de APIs (`fetch`)
- React Router (`BrowserRouter`, `Routes`, `Route`, `Link`, `useParams`)

Publicar em repositório público no GitHub com `README.md` contendo descrição, funcionalidades e conceitos utilizados.

* **Projeto desenvolvido:** [aula-09-projeto-react-02 (Catálogo de Cursos Online)](https://github.com/NicolasPureza/aula-09-projeto-react-02)

---

## 7. Referências

1. SOUZA, Natan. **Bootstrap 4: conheça a biblioteca front-end mais utilizada no mundo.** São Paulo: Casa do Código, 2018.
2. MACHADO, Kheronn Khennedy. **Angular 11 e Firebase: construindo uma aplicação integrada com a plataforma do Google.** São Paulo: Casa do Código, 2021.
3. EIS, Diego. **Guia Front-end: o caminho das pedras para ser um dev front-end.** São Paulo: Casa do Código, 2015.
4. GONÇALVES, Edson. **Desenvolvendo aplicações Web com JSP, Servlets, JavaServer Faces, Hibernate, EJB 3 Persistence e Ajax.** Rio de Janeiro: Ciência Moderna, c2007.
5. HARTCOPP, Patrícia Ferreira. **Métrica Web.** São Paulo: Contentus, 2020.
6. NIEDERAUER, Juliano. **Desenvolvendo Websites com PHP.** 3. ed. São Paulo: Novatec, 2017.
7. PREECE, J.; ROGERS, Y.; SHARP, H. **Design de Interação.** 3. ed. Porto Alegre: Bookman, 2013.
8. SOUSA, Roque Fernando Marcos. **Canvas HTML 5.** Rio de Janeiro: Brasport, 2014.

---
**Material de Apoio:** Disciplina de Frameworks Front-end — Prof. Me. Deivison S. Takatu (SENAI).
