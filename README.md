<h1>Anotações sobre NextJS</h1>
<h3>Arquivos especiais</h3>
<ul>
  <li>
    "loading.jsx"
    <li>Arquivo especial para carregamentos</li>
  </li>
  <li>
    "error.jsx"
    <li>Arquivo especial usado para mostrar mensagens de erros</li>
    <p>O arquivo de erro deve ser um Componente de Cliente, pois deve ser usado com Hooks como o useEffect
  </li>
  <p>Estes arquivos especiais devem estar dentro da pasta que corresponde à página na qual eu quero usá-los</p>
</ul>

<hr/>

<h1>Busca de Dados (Data Fetching)</h1>
<ul type="1">Há três tipos de formas de Buscar Dados:
  <li>Server Side Rendering (SSR)
    <p>Busca e renderiza os dados à cada solicitação do servidor, fazendo assim tudo ficar atualizado em tempo real.</p>
    
    ~~~javascript
      async function Page({params}) {
        const res = await fetch(`https://jsonplaceholder.typicode.com/posts/posts/${params.id}`, {cache: 'no-store'})
      };
      *const** data = await res.json()
    ~~~
    <p>Para usar o SSR, é necessário escrever <code>{cache: 'no-store'}</code> para o Next.js enteder.</p>
  </li>
  <li>Static Site Generation (SSG)
    <p>Automaticamente busca, salva e renderiza todo o conteúdo buscado de um Endopoint de uma API. Recomendado para projetos em que o conteúdo é frequentemente atualizado, como: Blogs, documentações e marketing pages.
  </li>
  <li>Incremental Static Generation
    <p>Combina os benefícios de SSR e SSG, permitindo Armazenar e então Renderizar Estaticamente os dados depois de um certo tempo dado, fazendo assim, os dados sempre os dados estarem atualizados.
  </li>
</ul>
<h1>Next.js API Endpoint</h1>
<p>Next.js n
