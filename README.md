# Criando-a-Sua-Primeira-API-Rest-com-Go

Vou criar um artigo sobre como desenvolver sua primeira API REST com Go, também conhecida como Golang. O artigo será estruturado em módulos para facilitar o entendimento e a organização do conteúdo.

---

## Introdução

Go é uma linguagem de programação poderosa e eficiente para o desenvolvimento de APIs REST. Com sua sintaxe simples e ferramentas robustas, Go é ideal para criar servidores web rápidos e confiáveis.

## Módulo 1: Configuração Inicial

Antes de começarmos, você precisa ter o Go instalado em sua máquina. Visite [golang.org](https://golang.org) para instruções de instalação.

## Módulo 2: Estrutura Básica de um Servidor Web

Vamos começar com a estrutura básica de um servidor web em Go.

```go
package main

import (
    "fmt"
    "log"
    "net/http"
)

func main() {
    http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
        fmt.Fprintf(w, "Olá, mundo!")
    })

    log.Println("Servidor rodando na porta 8080")
    log.Fatal(http.ListenAndServe(":8080", nil))
}
```

## Módulo 3: Implementando a API REST

Agora, vamos adicionar funcionalidades REST ao nosso servidor.

```go
package main

import (
    "encoding/json"
    "log"
    "net/http"
)

type Mensagem struct {
    Texto string `json:"texto"`
}

func main() {
    http.HandleFunc("/mensagem", mensagemHandler)

    log.Println("Servidor rodando na porta 8080")
    log.Fatal(http.ListenAndServe(":8080", nil))
}

func mensagemHandler(w http.ResponseWriter, r *http.Request) {
    switch r.Method {
    case "GET":
        json.NewEncoder(w).Encode(Mensagem{Texto: "GET realizado com sucesso"})
    case "POST":
        var msg Mensagem
        _ = json.NewDecoder(r.Body).Decode(&msg)
        json.NewEncoder(w).Encode(msg)
    default:
        w.WriteHeader(http.StatusMethodNotAllowed)
    }
}
```

## Módulo 4: Testando a API

Para testar a API, você pode usar ferramentas como `curl` ou Postman.

```bash
# Teste GET
curl http://localhost:8080/mensagem

# Teste POST
curl -X POST -d '{"texto":"Olá, API!"}' -H "Content-Type: application/json" http://localhost:8080/mensagem
```

## Conclusão

Você acabou de criar uma API REST simples com Go! Continue explorando e expandindo sua API para incluir mais métodos e recursos.

---

Espero que este artigo tenha ajudado a entender os passos básicos para criar uma API REST com Go. Pratique e não hesite em experimentar e adicionar novas funcionalidades à sua API.
