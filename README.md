# Java - trabalhando com exceções

Curso da alura para me aprofundar em java e exception, botarei conceitos para posterior consulta.

## Notas sobre curso

A pilha de execução em Java armazena informações sobre as chamadas de função em um formato Last In, First Out (LIFO). Cada vez que uma função é chamada, um novo quadro é adicionado ao topo da pilha. Quando a função é concluída, seu quadro é removido. A pilha de execução é fundamental para o fluxo de controle e o gerenciamento de chamadas de função no programa Java.

## O que ocorre quando quebra a pilha
Exceções, quando não tratada, retornam exceções que quebram o código, para previnir que tal situação ocorra, pode fazer o try-catch
```Java
 Usuario usuario = null;
                try {
                    System.out.println(usuario.nome);
                }
                catch (NullPointerException e){
                    System.out.println(e.getMessage());
                }

```
# IMPORTANTE

Você pode tratar execeções na chamada do método que ler a exceção, por exemplo, em um MVC, trato exeções dentro do service, na chamada do método eu uso o try, catch, além disso, quando for várias exeções, eu posso usar o "|" dentro do cacth, assim, evito vários caths seguidos para tratar várias exeções.
```Java
@PutMapping("/aprovar")
@Transactional
public ResponseEntity<String> aprovar(@RequestBody @Valid AprovarAdocaoDTO dto){
       try {
            this.service.aprovar(dto);
        }catch (EntityNotFoundException ex){
            return ResponseEntity.status(HttpStatus.NOT_FOUND).body("Adoção não encontrada");
        }
        return ResponseEntity.ok().build();
    }
    
    //service com as regras de negócio
ublic void solicitar(SolicitacaoDeAdocaoDTO dto){
    Pet pet = petRepository.getReferenceById(dto.idPet());
    if(pet.getAdotado()){
        throw new IllegalStateException("Pet já adotado");
    }
    Boolean petStatusAdocaco = adocaoRepository.existsByPetIdAndStatus(dto.idPet(), StatusAdocao.AGUARDANDO_AVALIACAO);
    if(petStatusAdocaco){
        throw new UnsupportedOperationException("Pet com adoção em andamento.");
    }
    Integer tutoAdocacoes = adocaoRepository.countByTutorIdAndStatus(dto.idTutor(), StatusAdocao.APROVADO);
    if (tutoAdocacoes == 2){
        throw new IllegalStateException("Tuto com o máximo adoções.");
    }
    Tutor tutor = tutorRepository.getReferenceById(dto.idTutor());

    adocaoRepository.save(new Adocao(tutor,pet, dto.motivo()));
}


```