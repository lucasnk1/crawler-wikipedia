# Trabalho de Web Crawler + 6 Graus de Separação

Integrantes:  
- **Augusto Kulzer**  
- **Lucas Leuck**  
- **Pedro Paccolo**

---

##  Sobre o trabalho
Esse projeto foi feito para a disciplina de Coleta, Preparação e Análise de Dados, e tem dois objetivos principais:

1. **Crawler de pessoas na Wikipédia**  
   - A gente criou um programa que começa pela página inicial da Wikipédia e vai navegando pelos links.  
   - Ele identifica se a página é de uma **pessoa real** (usando a infobox e categorias).  
   - Se for, salva o HTML da página na pasta `wikipedia_pessoas/`.  
   - No final, mostra quantas páginas foram visitadas e quantas realmente eram de pessoas.  

2. **Grau de separação entre pessoas**  
   - Com as páginas coletadas, montamos um **grafo** onde cada nó é uma pessoa.  
   - Se a página de uma pessoa tem link direto para outra, criamos uma conexão (aresta).  
   - Usamos **BFS (Busca em Largura)** para encontrar o **menor caminho** entre duas pessoas.  
   - O programa pede o nome da origem e destino, e mostra:  
     - O grau de separação (quantos passos de distância)  
     - O caminho completo (as pessoas intermediárias).  

---

## ⚙️ Requisitos e ambiente
- **Python 3.12** instalado  
- Bibliotecas necessárias:  
  pip install requests beautifulsoup4
  Recomenda-se rodar em um ambiente como Jupyter Notebook

---

##  Como rodar
1. Rodar primeiro a célula do crawler (`# CRAWLER`), ele vai coletar páginas da Wikipédia e salvar no diretório `wikipedia_pessoas`.  
   - Dá pra ajustar a quantidade de pessoas mudando `MAX_PESSOAS`.  
2. Depois rodar a célula (`# GRAFO`) que monta o grafo.  
3. Rode a céluca da (`# INTERFACE`) ele vai pedir dois nomes para calcular a separação e depois vai printar.


---

##  Exemplo de saída

GrGrafo construído: 994 pessoas, 2155 conexões.
✅ Grau de separação entre 'Henrique III de Castela' e 'Henrique V de Inglaterra': 3
Caminho encontrado:
   Henrique III de Castela (origem)
   Filipe II de Espanha
   Henrique VIII de Inglaterra
   Henrique V de Inglaterra (destino)


---

##  Dificuldades enfrentadas
- **Identificar se a página era mesmo de pessoa**:  
  Muitas páginas da Wikipédia têm categorias com “pessoas” no nome, mas não são de indivíduos (ex.: *Casamento entre pessoas do mesmo sexo*). Isso confundiu o crawler.  
- **Poucas conexões no começo**:  
  Quando coletamos só algumas páginas (tipo 5 ou 10), quase não apareciam links entre pessoas. Só começou a ficar interessante quando aumentamos para dezenas/centenas de páginas.  
- **Diferenças nos links**:  
  A Wikipédia usa variações nos URLs (maiúsculas, minúsculas, acentos, fragmentos `#`), então tivemos que normalizar os links pra não perder conexões.  
- **Tempo de execução**:  
  Como não dá pra “martelar” o servidor da Wikipédia, colocamos um `time.sleep` pra não sobrecarregar. Isso deixou a coleta mais demorada.  
- **Teste dos caminhos**:  
  Às vezes pedíamos duas pessoas e o programa dizia que não tinha conexão — na verdade o grafo ainda estava pequeno demais ou os links eram indiretos demais.  
- **Bloqueio de acesso sem cabeçalhos**:
No começo o site da Wikipédia bloqueava algumas requisições porque nosso crawler não tinha um cabeçalho de navegador. Tivemos que adicionar um `User-Agent` nos requests pra ele pensar que éramos um browser normal, senão dava erro e não baixava as páginas.

---

## 📂 Dados coletados

Os arquivos HTML coletados estão disponíveis na pasta `wikipedia_pessoas`.
Link para o repositório com dados coletados: ( https://github.com/lucasnk1/crawler-wikipedia/tree/main/wikipedia_pessoas )

---

##  Conclusão
O trabalho mostrou como funciona um crawler e como podemos modelar as relações entre páginas da Wikipédia em forma de grafo.  
A parte dos **6 graus de separação** conecta programação, teoria dos grafos e até sociologia 🤓.  

