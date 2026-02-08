
> 📌 Repositório público: https://github.com/pietrofarias/playdok

# Playdok (nome provisório)  
## Um schema aberto para ler, interpretar e encenar textos

Playdok **não é uma aplicação**.  
É um **schema de documento**.

A proposta é definir um **tipo de documento narrativo e encenável**, que possa ser criado, armazenado e lido por qualquer aplicação, da mesma forma que PDF é um tipo de documento — independentemente do leitor.

A ideia é simples:

> Alguém escreve um Playdok.  
> Outra pessoa abre e interpreta.  
> A ferramenta não importa.

---

## O problema que o Playdok tenta resolver

Textos performáticos (stand-up, teatro, monólogos, roteiros) carregam muito mais do que palavras:

- intenção
- ritmo
- pausas
- ações
- dependência entre falas
- estrutura temporal

Roteiros tradicionais resolvem **a leitura**, mas falham em **explicar a intenção do autor**.  
Quando o autor tenta explicar mais, o roteiro vira poluído.  
Quando explica menos, é mal interpretado.

Playdok nasce para resolver esse conflito.

---

## O que é o Playdok

Playdok é um **schema de documento narrativo e encenável**.

Ele pode representar:
- stand-up comedy  
- roteiro teatral  
- roteiro comercial  
- monólogo  
- poesia performática  
- qualquer texto pensado para ser **dito, encenado ou performado**

O documento deve:
- ser **lido facilmente como um roteiro**
- permitir **camadas adicionais** de intenção do autor
- manter a leitura limpa por padrão

---

## Ideia central

> Ler um Playdok deve ser como assistir a um filme  
> com os comentários do diretor ligados —  
> com a opção de desligar tudo e ainda entender o filme.

O autor escreve uma vez.  
O leitor escolhe **quanto quer ver**.

---

## Abordagem técnica (alto nível)

- **XML** é usado como base estrutural do schema
- **Markdown** é usado como camada de leitura humana
- O documento separa claramente:
  - estrutura técnica (analisável por máquinas)
  - narrativa legível (focada em humanos)

O XML não é pensado para ser “bonito”.  
O Markdown é.

---

## `printView`: contrato de leitura humana

Todo documento Playdok **deve conter um `printView`**.

- `printView` é escrito em **Markdown**
- Fica dentro de um **CDATA**
- Pode conter HTML compatível com Markdown (`<details>`, `<summary>`)

Ele existe para:
- leitura rápida
- ensaio
- impressão
- interpretação humana

Exemplo simplificado:

```markdown
==O meu superpoder é a adaptação social.==

Sou bom nisso?

*(balanço a cabeça: não)*

==Sou péssimo. Mas funciona.==
```

Ações e intenções podem existir, mas ficam **ocultáveis**.

---
## Estrutura do documento (resumida)

Um `document.xml` Playdok contém:

-   `document` (raiz)
    
    -   `lineage` — origem e forks do documento
        
    -   metadados básicos (autor, título, data)
        
    -   `printView` — leitura humana
        
    -   `premisse` — premissa inicial
        
    -   `timeline`
        
        -   `beat` (ordenado)
            
            -   texto
                
            -   pausas
                
            -   ações (act-outs)
                
            -   notas de intenção
                

Essa separação permite:

-   leitura simples
    
-   análise estrutural
    
-   relatórios futuros
    
-   interoperabilidade entre ferramentas

----------

## Linhagem e forks

O Playdok carrega **linhagem mínima** no próprio documento:

-   repositório de origem
    
-   documento raiz
    
-   documento pai (em caso de fork)
    

Histórico de commits, comentários e socialização **não ficam no documento**.  
Isso é responsabilidade de outros serviços.

Essa decisão permite, no futuro:

-   rastrear autoria
    
-   criar cadeias de forks
    
-   ancorar versões em blockchain, se desejado
    

----------

## Para quem é este projeto

Playdok é feito **para autores**.

Desenvolvedores são bem-vindos,  
mas o schema não nasce da tecnologia — nasce da escrita.

O foco são:

-   roteiristas
    
-   comediantes
    
-   escritores
    
-   pessoas que trabalham com performance e encenação
    

São essas pessoas que definem:

> o que precisa existir no schema.

----------

## Estrutura atual do repositório

O repositório está em fase inicial e hoje contém:

        
-   `/Documentation/Samples`
    
    -   exemplos reais de documentos
        
    -   visualização em Markdown
        
    -   textos usados como prova de conceito
        
E o schema inicial, está na raiz do projeto.

Nada aqui é definitivo.  
Tudo é discutível.


----------

## O que estou buscando agora

Feedback conceitual.

-   O schema é compreensível para quem escreve?
    
-   É simples para quem só lê?
    
-   Os conceitos estão bem nomeados?
    
-   O que está faltando?
    
-   O que está sobrando?
    

Este repositório existe para **evoluir o schema em público**.

----------

## Estado atual

-   ✅ Schema inicial definido (v0.1)
    
-   ✅ Documento de exemplo funcional
    
-   ✅ Visualização via Markdown
    
-   ⏳ Nome definitivo (Playdok é provisório)
    
-   ⏳ Validação formal do schema
    
-   ⏳ Ferramentas e visualizadores externos
    



---

## Próximos passos (abertos à comunidade)

Nada aqui está fechado. Os próximos passos **dependem da discussão**:

- Refinar o vocabulário do schema  
- Ajustar a granularidade dos `beats`
- Evoluir a separação entre:
  - texto
  - ação
  - intenção
- Avaliar estratégias de validação (XSD, Relax NG, Schematron)
- Pensar interoperabilidade com outros formatos existentes

O objetivo não é “chegar rápido”,  
é **chegar certo**.

---

## O que o Playdok não é

Para deixar claro desde o início:

- ❌ não é um editor
- ❌ não é um app de escrita
- ❌ não é um formato proprietário
- ❌ não é uma plataforma fechada

Playdok é um **schema aberto**.

Ferramentas podem nascer em volta dele,  
mas o schema precisa sobreviver a todas elas.

---

## Por que XML (e não JSON)

XML foi escolhido por motivos práticos:

- hierarquia explícita
- validação madura
- suporte nativo a CDATA
- clareza semântica para documentos complexos
- longevidade como formato de arquivo

Nada impede:
- exportar para JSON
- criar camadas de ETL
- mapear para bancos relacionais

Mas o **contrato canônico** começa no XML. É definitivo? Claro que não. Apenas o que minha limitação conseguiu aplicar até o momento.

---

## Sobre leitura vs estrutura

Uma regra guia o projeto:

> O que é para humanos lerem  
> não deve ser difícil por causa da máquina.

Por isso:
- estrutura fica fora do `printView`
- narrativa fica dentro do `printView`
- CDATA preserva exatamente o texto do autor

Máquinas analisam a estrutura.  
Pessoas leem a história.

---

## Contribuições

Este projeto precisa de:

- feedback conceitual
- revisão de nomenclatura
- exemplos reais de uso
- críticas honestas

Pull requests são bem-vindos,  
mas **discussões também contam como contribuição**.

Se você escreve roteiros, textos performáticos ou histórias encenáveis,  
sua visão é especialmente importante aqui.

---

## Licença e abertura

O schema é aberto por princípio.

A ideia é que ele possa ser:
- estudado
- adaptado
- estendido
- usado em qualquer contexto

Sem dependência de ferramenta, empresa ou plataforma.

---

## Encerramento

Playdok é uma tentativa de criar um **idioma comum**  
entre quem escreve, quem interpreta e quem constrói ferramentas.

Ainda é cedo.  
Ainda é imperfeito.

Mas é público, aberto e vivo —  
e isso é intencional.

Se isso faz sentido para você,  
bem-vindo à conversa.
