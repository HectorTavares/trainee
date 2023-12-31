# Naruto - entities.Batalha entities.Ninja

![cover photo](https://s.aficionados.com.br/imagens/frases-iconicas-dos-personagens-de-naruto_f.jpg)

Para quem não conhece, Naruto é uma série de anime e mangá criada por Masashi Kishimoto que recebeu adaptação para animê em 2002. A trama gira em torno de Naruto Uzumaki, um jovem entities.Ninja que constantemente procura por reconhecimento e tem o sonho de se tornar um Hokage, o líder máximo e mais poderoso de sua vila. Durante a história, ocorrem diversas batalhas Ninjas em prol de algum objetivo, tais como: exames para subir de nível, guerras, missões, entre outras.

Neste exercício, vamos modelar e simular uma batalha entre dois nijas. Leia atentamente as regras e transforme tudo o que está sendo solicitado em classes Java respeitando os princípios da OO que vimos até aqui.

## entities.Jutsu

entities.Jutsu (術; Literalmente significa "habilidades/técnicas") são as artes místicas que um entities.Ninja utiliza na batalha. Para usar uma técnica, o entities.Ninja precisará usar seu chakra. Neste exercício, vamos considerar o chakra como a energia que o entities.Ninja gasta para se manter vivo e atacando.

### Modelagem

1. Modele uma classe entities.Jutsu que possui como atributos a quantidade de chakra que consome quando utilizado e o dano (quantidade de chakra que abate do oponente).
2. Todos os atributos devem ser informados no momento em que o entities.Jutsu é instanciado e não pode ser alterado posteriormente.
3. Sobre o atributo que se refere a quantidade de chakra consumido pelo entities.Jutsu, ele deve ser do tipo `int` e valor 5 deve deve ser o máximo que pode ser atribuído.
4. Sobre o atributo que se refere ao dano (quantidade de chakra que o entities.Jutsu remove do oponente), ele deve ser do tipo `int` e valor 10 deve deve ser o máximo que pode ser atribuído.

## entities.Ninja

Ninjas são o foco principal e a principal potência militar na série. A maioria vem de uma aldeia oculta, alguns dos quais vêm de clãs entities.Ninja especializados, e irão realizar as batalhas do nosso exercício.

### Modelagem 

1. Modele uma classe entities.Ninja que possui como atributos o nome, o chakra que possui e o seu entities.Jutsu principal.
2. Todos os atributos devem ser informados no momento em que o entities.Ninja é instanciado.
1. O chakra do entities.Ninja deve ser do tipo `int` e inicializar com valor 100.
3. O entities.Ninja deve possuir um método `atacar` que recebe como parâmetro o seu entities.Ninja oponente. 
4. O entities.Ninja deve possuir um método `receberGolpe` que recebe por parâmetro um valor do tipo `int` correspondente ao dano do golpe recebido.
5. O método `atacar` deve invocar o método `receberGolpe` do oponente, informando o dano do entities.Jutsu principal do entities.Ninja.
6. O metodo `receberGolpe` deve abater do chakra do entities.Ninja o valor do dano recebido.
7. Quando atacar um oponente, o valor do chakra deve ser atualizado de acordo com o consumo do entities.Jutsu.


## entities.Batalha
1. Modele uma classe entities.Batalha na qual **o único** método público deverá ser o `lutar` que receberá como parâmetro os dois nijas da luta. Segue exemplo de assinatura do método:  `public entities.Ninja lutar(entities.Ninja primeiroNinja, entities.Ninja segundoNinja)`.
2. No método `lutar`, cada entities.Ninja ataca o seu oponente 3 vezes.
3. O método `lutar` deve retornar como entities.Ninja vencedor aquele que possuir o maior chakra ao final da luta.
5. Se houver empate, o entities.Ninja do primeiro parâmetro deve ser retornado como vencedor.

## Regras Gerais

### Uchiha Itachi
![Itachi](https://vignette.wikia.nocookie.net/liberproeliis/images/b/b0/Itachi_render_by_xuzumaki-d49n7va.png/revision/latest/scale-to-width-down/340?cb=20161119225550&path-prefix=pt-br)

Se um dos Ninjas se chamar **Itachi**, ele deve vencer sempre, independentemente do oponente. **Obs: não ouse afirmar que ele não é o melhor de todos.**

### Exemplos de Teste

```Java
@NinjaTest
public void deveRetornarNinjaComJutsuMaisForteSeOsDoisGastamOMesmoChakraParaAtacar(){
    entities.Jutsu jutsuNinjaUm = new entities.Jutsu(5, 10);
    entities.Ninja ninjaUm = new entities.Ninja("Naruto", jutsuNinjaUm);

    entities.Jutsu jutsuNinjaDois = new entities.Jutsu(5, 8);
    entities.Ninja ninjaDois = new entities.Ninja("Gaara", jutsuNinjaDois);

    entities.Batalha batalha = new entities.Batalha();

    entities.Ninja ninjaVencedor = batalha.lutar(ninjaUm, ninjaDois);

    Assert.assertSame(ninjaUm, ninjaVencedor);
}

@NinjaTest
public void deveAtualizarOChakraDoOponenteDeAcordoComODanoDoJutsoQuandoAtacar() {
    entities.Jutsu jutsuNinjaAtacante = new entities.Jutsu(5, 10);
    entities.Ninja ninjaAtacante = new entities.Ninja("Naruto", jutsuNinjaAtacante);

    entities.Jutsu jutsuNinjaOponente = new entities.Jutsu(5, 8);
    entities.Ninja ninjaOponente = new entities.Ninja("Gaara", jutsuNinjaOponente);

    int nivelChakraEsperado = 90;

    ninjaAtacante.atacar(ninjaOponente);

    Assert.assertEquals(nivelChakraEsperado, ninjaOponente.getChakra());
}

```

# Referências
[Sobre a série](https://naruto-pedia.fandom.com/pt-br/wiki/Naruto_(S%C3%A9rie))

[Chakra](https://naruto.fandom.com/pt-br/wiki/Chakra)

[entities.Jutsu](https://naruto.fandom.com/pt-br/wiki/Jutsu)

## NinjaTest Obrigatórios

* Devem existir **obrigatóriamente** na solução entregue testes unitários com os seguintes nomes:

    - deveRetornarNinjaComJutsuMaisForteSeOsDoisGastamOMesmoChakraParaAtacar
    - deveAtualizarOChakraDoOponenteDeAcordoComODanoDoJutsoQuandoAtacar
    - deveRetornarPrimeiroNinjaComoVencedorQuandoONomeForItachi
    - deveRetornarSegundoNinjaComoVencedorQuandoONomeForItachi
    - deveRetornarPrimeiroNinjaComoVencedorQuandoEmpatar
