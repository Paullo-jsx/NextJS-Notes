<h1>Arquivos especiais do Next.js </h1>

<ul>
  <li>
    <h4>loading.jsx</h4>
    <ul>
      <li>Arquivo especial para carregamentos na página atual</li>
    </ul>
  </li>
  <li>
    <h4>error.jsx</h4>
    <ul>
      <li>Arquivo especial usado para mostrar mensagens de erros na página atual</li>
      <li>O arquivo de erro deve ser um Componente de Cliente, pois deve ser usado com Hooks como o useEffect</li>
    </ul>
  </li>
</ul>

``
Os arquivos especiais devem estar dentro da pasta que corresponde à página na qual eu quero usá-los. Exemplo abaixo:
``

```
app
│ ╰─ second_page (pasta que corresponde à uma página)
│ │     ├╴ page.jsx
│ │     ├╴ loading.jsx
│ │     ├╴ error.jsx
│ ╰─ third_page (pasta que corresponde à outra página)
│       ├╴ page.jsx
│       ├╴ loading.jsx
│       ├╴ error.jsx
│
page.js (primeira página carregada)
layout.js
globals.css
```
<hr/>

<h1>Busca de Dados (Data Fetching) (SSR, SSG, ISG)</h1>
<ol type="1"><h2>Há três tipos de formas de Buscar Dados:</h2>
  <li><h3>Server Side Rendering (SSR)</h3>
    <p>Busca e renderiza os dados à cada solicitação do servidor, fazendo assim tudo ficar atualizado em tempo real. Exemplo abaixo: </p>

   ````javascript
async function Page({params}) {
        const res = await fetch(`https://jsonplaceholder.typicode.com/posts/posts/${params.id}`, {cache: 'no-store'})
      };
      const data = await res.json()
````

``Para o Nexts.js reconhecer que isso é uma rota SSR é necessário ter o {cache: 'no-store'}``

  </li>
 
  <li><h4>Static Site Generation (SSG)</h4>
    <p>Automaticamente busca, salva e renderiza todo o conteúdo buscado de um Endopoint de uma API. Recomendado para projetos em que o conteúdo não é frequentemente atualizado, como: Blogs, documentações e marketing pages. Exemplo abaixo: </p>

```javascript
   async function Page({params) {
        const res = await fetch(`https://jsonplaceholder.typicode.com/posts/posts/${params.id}`)
   };
   const data = await res.json()
```

`Para o Next.js identificar que isso é uma rota SSG, não deve ser adicionado nada dentro da variável que tem o Endpoint da API`

  </li>
  <li><h4>Incremental Static Generation (ISR) </h4>
    <p>Combina os benefícios de SSR e SSG, permitindo Armazenar e então Renderizar Estaticamente os dados depois de um certo tempo dado, fazendo assim, os dados sempre os dados estarem atualizados. </p>

  ```javascript
    async function Page() {
        const res = await fetch(`https://jsonplaceholder.typicode.com/posts/posts/${params.id}`, {next: {revalidate: 10}})
    };
    const data = await res.json()
  ```
  
  </li>
</ol>
