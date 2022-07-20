# webhook-criacao-do-novo-academico

## Documentação Novo Acadêmico:
*No novo modelo do acadêmico da Bonsae, pense na estrutura de cadastro das Turmas em 4 "caixas": Período Letivo > Turmas > Disciplinas > Práticas. O Período Letivo detém as datas de início e fim das turmas que, consequentemente influenciam as datas de início e fim das disciplinas e práticas vinculadas a elas. Esclarecendo a orientação acima, é possível puxar as informações das práticas a qualquer momento ou configurar para que os dados sejam puxados ao final de um período letivo.

 OBS.: Primeiramente deve-se ter um Período Letivo Cadastrado no Sistema, e ele deve ter data inicial e final que englobem todas as outras. Ou seja, nenhuma outra data cadastrada deve começar antes da data inicial do período, nem terminar depois da data final do mesmo.
 
 *"instancia" nas URLs abaixo se referem ao nome da IES, campus ou unidade que a insituição irá implantar a Bonsae. De acordo com a quantidade de campus, a URL pode ter um ou dois formatos. Exemplo de formatos.: "[unit.bonsae.com.br](http://unit.bonsae.com.br)" ou "[unit.aracaju.bonsae.com.br](http://unit.aracaju.bonsae.com.br)". Confirme com a coordenação do curso ou com a própria equipe Bonsae qual dos dois formatos será utilizado para o seu caso específico.

### Criação de Período Letivo:

##### Rota - POST: 
#
> url:[https://instancia.bonsae.com.br/api/webhook/create-school-period](https://instancia.bonsae.com.br/api/webhook/create-school-period)

##### Dados a serem enviados:

#
| variável | tipo | Descrição |
| --- | --- | --- |
| token | string | Token de acesso |
| name | string | Nome do Período, para identificação |
| school_period | string | Período Letivo (1° Semestre, 2° Semestre, 1° Semestre 1° Bimestre, 1° Semestre 2° Bimestre, 2° Semestre 1° Bimestre ou 2° Semestre 2° Bimestre) |
| start_date | date | Quando o período inicia |
| final_date | date | Quando o período finaliza |

### Criação de Turma:

##### Rota - POST: 
#
> url:[https://instancia.bonsae.com.br/api/webhook/create-class](https://instancia.bonsae.com.br/api/webhook/create-class)

##### Dados a serem enviados:

#
| variável | tipo | Descrição |
| --- | --- | --- |
| token | string | Token de acesso |
| schoolPeriod | string | Nome do Período Letivo |
| name | string | Nome da Turma |
| code | string | Código da Turma |
| start_date | date | Quando a turma inicia |
| end_date | date | Quando a turma finaliza |
| category | string | Categoria da turma (NPJ, Curso ou TCC) |
| period | string | Período da turma (1°, 2°, 3°, 4°, 5°, 6°, 7°, 8°, 9° ou 10°) |
| campus_name | string | Campus que a Turma pertence |
| campus_uf | string | UF do estado do Campus |

### Criação de Disciplina:

##### Rota - POST: 
#
> url:[https://instancia.bonsae.com.br/api/webhook/create-discipline](https://instancia.bonsae.com.br/api/webhook/create-discipline)

##### Dados a serem enviados:

#
| variável | tipo | Descrição |
| --- | --- | --- |
| token | string | Token de acesso |
| name | string | Nome da Disciplina |
| code | string | Código da Disciplina |
| shift | string | Turno da Disciplina (Matutino, Vespertino ou Noturno) |
| class_code | string | Código da Turma, a que a Disciplina pertence |

##### OBS.: Para o funcionamento dos passos a seguir, já devemos ter cadastrado no sistema as disciplinas e os usuários a serem adicionados.

### Adicionar Professor a Disciplina:

##### Rota - POST: 
#
> url:[https://instancia.bonsae.com.br/api/webhook/add-teacher-in-class](https://instancia.bonsae.com.br/api/webhook/add-teacher-in-class)

##### Dados a serem enviados:

#
| variável | tipo | Descrição |
| --- | --- | --- |
| token | string | Token de acesso |
| code | string | Código da Disciplina |
| teacherEmail | string | Email do professor |

### Remover Professor da Disciplina:

##### Rota - POST: 
#
> url:[https://instancia.bonsae.com.br/api/webhook/remove-teacher-in-class](https://instancia.bonsae.com.br/api/webhook/remove-teacher-in-class)

##### Dados a serem enviados:

#
| variável | tipo | Descrição |
| --- | --- | --- |
| token | string | Token de acesso |
| code | string | Código da Disciplina |
| teacherEmail | string | Email do professor |

### Adicionar Aluno a Disciplina:

##### Rota - POST: 
#
> url:[https://instancia.bonsae.com.br/api/webhook/add-student-in-class](https://instancia.bonsae.com.br/api/webhook/add-student-in-class)

##### Dados a serem enviados:

#
| variável | tipo | Descrição |
| --- | --- | --- |
| token | string | Token de acesso |
| code | string | Código da Disciplina |
| studentEmail | string | Email do aluno |

### Remover Aluno da Disciplina:

##### Rota - POST: 
#
> url:[https://instancia.bonsae.com.br/api/webhook/remove-student-in-class](https://instancia.bonsae.com.br/api/webhook/remove-student-in-class)

##### Dados a serem enviados:

#
| variável | tipo | Descrição |
| --- | --- | --- |
| token | string | Token de acesso |
| code | string | Código da Disciplina |
| studentEmail | string | Email do aluno |

##### Exemplo Resposta Sucesso:
#
Para qualquer uma das rotas acima citadas, o retorno em caso de sucesso da requisição seguirá o mesmo formato. Será um json contendo os dados que foram passados para a criação do método específico.

###### Criação de uma turma:

#
```sh
{
    "token":"auth_token_api_274319732!", 
    "name":"Turma 001", 
    "code":"T001", 
    "start_date":"11/07/2022", 
    "end_date":"21/10/2022", 
    "category":"Curso", 
    "period":"9\u00b0", 
    "campus_name":"rio de janeiro", 
    "campus_uf":"RJ"
}
```
##### Exemplo de erros:
#
Token diferente ao permitido
"YOU_NOT_ACCESS"

Alguma informação fora do padrão, 
"ERROR_IN_REQUEST"
