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
<ol type="1"><h2>Há três tipos de formas de Buscar Dados: SSR, SSG, ISR.</h2>

``
Abaixo está a estrutura de pastas onde está o arquivo que irá ter o código.
``

```
app
│ ╰─ api (pasta onde irá ter a página onde os dados serão buscados)
│    ╰─ users (pasta da página onde os dados serão renderizados ao usuário)
│       ├╴ route.js (arquivo onde os dados serão buscados)
│
│
page.js (primeira página carregada)
layout.js
globals.css
```

  <li><h3>Server Side Rendering (SSR)</h3>
    <p>Busca e renderiza os dados à cada solicitação do servidor, fazendo assim tudo ficar atualizado em tempo real. Exemplo abaixo: </p>

  ``
  (app/api/users/route.jsx)
  ``
   
   ````javascript
async function User({titulo}) {
    const buscar = await fetch(`https://api.github.com/users/Paullo-jsx/repos/${titulo.title}`, {cache: 'no-store'});
    const armazena = await buscar.json()
    
    return (
      <main>
        {armazena.titulo}
      </main>
    )
}
````

``Para o Nexts.js reconhecer que isso é uma rota SSR é necessário ter o {cache: 'no-store'} na variável onde é buscado os dados.``

  </li>
 
  <li><h3>Static Site Generation (SSG)</h3>
    <p>Automaticamente busca, salva e renderiza todo o conteúdo buscado de um Endopoint de uma API. Recomendado para projetos em que o conteúdo não é frequentemente atualizado, como: Blogs, documentações e marketing pages. Exemplo abaixo: </p>

  ``
  (app/api/users/route.jsx)
  ``
   
```javascript
   async function Page({titulo}) {
      const buscarDados = await fetch(`https://api.github.com/users/Paullo-jsx/repos/${titulo.title}`);
      const armazenaDados = await buscarDados.json()

      return (
         <main>
            {armazenaDados.titulo}
         </main>
      )
   }
```

`Para o Next.js identificar que isso é uma rota SSG, não deve ser adicionado nada dentro da variável que tem o Endpoint da API`

  </li>
  <li><h3>Incremental Static Generation (ISR) </h3>
    <p>Combina os benefícios de SSR e SSG, permitindo Armazenar e então Renderizar Estaticamente os dados depois de um certo tempo dado, fazendo assim, os dados sempre os dados estarem atualizados. </p>

  ``
  (app/api/users/route.jsx)
  ``
   
  ```javascript
       async function Page({titulo}) {
      const buscarDados = await fetch(`https://api.github.com/users/Paullo-jsx/repos/${titulo.title}`, {next: {revalidate: 10}});
      const armazenaDados = await buscarDados.json()

      return (
         <main>
            {armazenaDados.titulo}
         </main>
      )
   }
  ```
  
  </li>
</ol>
