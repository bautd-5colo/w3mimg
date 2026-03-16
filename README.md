# Aviso

Deixando claro: o texto abaixo se apoia num curso gratuito e o material dele não pode ser redistribuído. Se o tema interessar, procure o curso aberto da trilha de Java com Spring Boot. Se a plataforma sair do ar ou começar a cobrar, isso não está no meu alcance — mas o conteúdo é ótimo e quem assina um plano aproveita bem mais.

# Introdução

Dentro do módulo web do framework existem duas partes:

- a camada MVC web;
- a construção de APIs REST.

Aqui o assunto é montar uma API REST, e no caminho aparecem peças como os controladores REST.

Foi apresentado o modelo de maturidade de REST, com seus níveis:

![levels - glory of rest](images/niveis-de-maturidade.png)

Também foi comentado o princípio de hipermídia como motor do estado da aplicação:

![hateoas](images/hipermídia.png)

O pacote inicial de API REST já traz um servidor embutido escutando na porta 8080.

O professor usou o gerador de projetos com a configuração mostrada abaixo.

![Initializer used](images/gerador-usado.png)

Gerei um projeto parecido (o site do gerador mudou um pouco). O arquivo compactado e a pasta com o conteúdo extraído estão na raiz do repositório.


## Rodando o projeto básico

Rodar o projeto básico não foi tão simples; gravei um vídeo sobre essa dificuldade.

O comando para subir a aplicação no terminal, a partir da raiz deste repositório, é:

```
cd my-first-web-api-project-generated-with-initializr/
mvn spring-boot:run
```

Comentário: basta esperar alguns segundos. O terminal não imprime novas mensagens. A aplicação fica acessível no endereço da máquina local na porta 8081.

Outro comentário: testei parar a aplicação e subir de novo, e funcionou.


## Controlador REST

Gravei um vídeo sobre a criação do controlador REST e de uma rota de leitura.

Anotações úteis num controlador REST:

![some annotations](images/anotacoes.png)


Resumo das anotações:

- a anotação de controlador REST indica que a classe recebe requisições REST;
- a anotação de mapeamento na classe define o prefixo das rotas dos métodos;
- as anotações por verbo correspondem a cada operação HTTP;
- a anotação de corpo indica que o JSON recebido será convertido num objeto;
- a anotação de variável de caminho captura um valor que vem pela URL da requisição.

Também gravei um vídeo explicando a API que criamos.

O link da aula em que esse conteúdo foi apresentado está publicado na plataforma.


## Documentação interativa

Gravei um vídeo sobre o processo de adicionar a configuração de documentação ao projeto.

Uma resposta pública num fórum de programação me indicou a dependência que resolveu o problema da janela da ferramenta reclamando do endereço base. Com isso o manifesto de build ganhou três dependências novas: duas da biblioteca de documentação e uma para esse ajuste.

Em vários tutoriais aparece uma classe de configuração chamada Docket, sem explicar bem o que ela é; a aula mostrou a importação dela.

Existem também alguns artigos na web explicando como habilitar a documentação num projeto do framework.

O endereço da interface gerada fica no caminho de documentação da aplicação.

Numa aula seguinte o professor detalha como personalizar itens da documentação numa classe de configuração.

A documentação não deve conhecer as regras de negócio nem as classes de modelo, e sim a interface exposta ao mundo externo, ou seja, os controladores. A imagem mostra como limitar quais classes entram na documentação.

![Classes to be analyzed by Swagger](images/classes-analisadas.png)

Para detalhes como personalizar informações de contato, vale assistir à aula indicada.

No teste de criação de usuário, a imagem mostra como personalizar os parâmetros do corpo da requisição:

![personalizing request body](images/corpo-personalizado.png).

Comentário: dá para imprimir os dados recebidos no console onde a aplicação está rodando, usando uma chamada de impressão.

Incluí métodos com as anotações necessárias para cobrir as outras operações e completar as tarefas de CRUD. A classe final do controlador ficou assim:

```
package dio.my_first_web_api.controller;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.PutMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

import dio.my_first_web_api.model.Usuario;
import dio.my_first_web_api.repository.UsuarioRepository;

@RestController
@RequestMapping("/usuarios")
public class UsuarioController {
    @Autowired
    private UsuarioRepository repository;

    public String getMethodName(@RequestParam String param) {
        return new String();
    }

    @GetMapping()
    public List<Usuario> obterUsuarios() {
        return repository.findAll();
    }

    @DeleteMapping("/{id}")
    public void delete(@PathVariable("id") Integer id) {
        repository.deleteById(id);
    }

    @PostMapping("/novo")
    public void adicionarUsuario(@RequestBody Usuario usuario) {
        System.out.println(usuario);
        System.out.println("adicionando um usuário");
    }

    @PutMapping("/edit")
    public void editarUsuario(@RequestBody Usuario usuario) {
        System.out.println(usuario);
        System.out.println("editando um usuário");
    }
}
```

Também gravei um vídeo sobre o uso de exceções numa aplicação do framework.

O código do capítulo está num repositório público da trilha.