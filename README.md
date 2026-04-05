>1. A Fronteira entre o Desenvolvimento de Código e a Engenharia
````
O texto inicial estabelece uma separação essencial entre o ato de "codificar" e a disciplina de engenharia. O autor argumenta que, embora os conceitos de "Programação" e "Engenharia de Software" sejam frequentemente tratados como equivalentes, eles possuem níveis de exigência distintos.

A programação é descrita como uma tarefa de construção imediata que, em muitos casos, carece de diretrizes rigorosas. Em contrapartida, a Engenharia de Software é apresentada como a aplicação de fundamentos científicos para projetar soluções robustas, exatas e confiáveis. O foco reside na necessidade de profissionalismo no setor: assim como cálculos falhos em projetos aeroespaciais levam a catástrofes, a infraestrutura digital moderna — que sustenta a sociedade atual — demanda métodos muito mais criteriosos do que o desenvolvimento de scripts convencionais.
````
>2. O Papel da Longevidade e a Resiliência do Software
````
Na sequência, a definição de Engenharia de Software incorpora a variável cronológica como fator determinante.
Análise: Enquanto a programação foca na resolução de um gargalo pontual (a entrega do código), a engenharia dedica-se a "manter essa lógica funcional e rentável ao longo de grandes períodos". Isso exige processos estruturados, ferramentas de ponta e uma mentalidade corporativa voltada para a evolução constante. O triunfo de um projeto não termina no seu lançamento; ele depende da sua SUSTENTABILIDADE: o poder de um sistema se transformar conforme o mercado muda, ganhar escala com o crescimento da empresa e sobreviver a todo o seu ciclo de existência, da implementação inicial até a sua eventual descontinuação.
````
>3. Requisitos Não Funcionais: Os Atributos de Qualidade
````
Diferentemente das funcionalidades básicas (o que a aplicação entrega), os requisitos não funcionais determinam as propriedades e restrições do sistema — ou seja, a maneira como ele opera.

1-Eficiência (Desempenho): Trata da rapidez e do tempo de resposta da plataforma. Estabelece parâmetros como o limite de segundos para o carregamento de uma interface ou a taxa de processamento de grandes volumes de transações.
2-Confiabilidade (Disponibilidade): Refere-se à constância com que o serviço permanece ativo para o público. Um exemplo prático é a meta de uptime de 99,9%, assegurando que a plataforma sofra o mínimo possível de interrupções ou quedas.
3-Capacidade de Expansão (Escalabilidade): É o potencial do software de absorver um fluxo crescente de acessos ou dados sem perder qualidade. Isso pode ser feito através do reforço de hardware ou da distribuição de carga entre vários servidores.
4-Proteção (Segurança): Foca em blindar a arquitetura contra invasões e vulnerabilidades. Garante que as informações sejam mantidas em sigilo, preservando a privacidade e a veracidade dos dados armazenados.
5-Facilidade de Uso (Usabilidade): Diz respeito à experiência do indivíduo ao navegar pelo sistema. Uma ferramenta com alta usabilidade é aquela que se mostra lógica e simples, minimizando a necessidade de manuais complexos.
````
>4. Cenários de Trade-offs
````
1. Proteção vs. Facilidade de Uso
Contexto: Uma plataforma de finanças que impõe múltiplas camadas de verificação (digital, código secreto e leitura facial) para cada operação.

Análise: Embora o nível de SEGURANÇA atinja um patamar rigoroso contra fraudes, a EXPERIÊNCIA DO USUÁRIO é comprometida. O excesso de barreiras torna a navegação burocrática e frustrante para o cliente no dia a dia.

2. Acesso Contínuo vs. Integridade de Dados
Contexto: Uma rede de servidores globais tentando sincronizar informações durante uma instabilidade técnica.

Análise: Se o foco for a CONSISTÊNCIA, o sistema impedirá qualquer alteração até que todos os nós estejam alinhados (sacrificando o tempo de resposta). Se o foco for a DISPONIBILIDADE, o serviço permanece ativo para o público, porém com o risco de exibir dados divergentes entre diferentes regiões até que a conexão seja restabelecida.

3. Eficiência vs. Orçamento
Contexto: Acelerar o processamento de um portal para que as páginas carreguem instantaneamente via hardware de última geração.
````
>5. Programa com sintaxe correta, mas com a lógica errada (j+1=>j-1).
````
1.

R: Não é possivel testar individualmente cada caso, pois existem 65535 casos de entrada;

2. Quantos erros apontam para o problema de lógica?

R: 4

3. Quais são?

R: -29999; 29999; -30000; e 30000.
````
>6. Exercicio sobre um sistema de "Biblioteca".
````
package Main;

import java.util.ArrayList;
import java.util.Scanner;

public class Padaria {
    public static void main(String[] args) {
        Scanner leitor = new Scanner(System.in);
        ArrayList<Produto> vitrineProducao = new ArrayList<>();
        int opcao = 0;

        System.out.println("--- Sistema de Produção: Padaria Java ---");

        do {
            System.out.println("\n1. Cadastrar Novo Item (Massa)");
            System.out.println("2. Ver Vitrine de Produção");
            System.out.println("3. Assar Fornada (Finalizar Item)");
            System.out.println("4. Sair");
            System.out.print("Escolha uma opção: ");

            // Uma pequena melhoria para evitar erros se o usuário digitar letras
            if (!leitor.hasNextInt()) {
                System.out.println("Por favor, digite um número válido.");
                leitor.next();
                continue;
            }

            opcao = leitor.nextInt();
            leitor.nextLine();

            switch (opcao) {
                case 1:
                    System.out.print("Nome do Alimento: ");
                    String nome = leitor.nextLine();
                    System.out.print("Categoria (Pão, Bolo, Salgado): ");
                    String categoria = leitor.nextLine();
                    boolean add;
                    if (vitrineProducao.add(new Produto(nome, categoria))) {
                        add = true;
                    } else add = false;
                    System.out.println("Item enviado para a área de preparo!");
                    break;

                case 2:
                    System.out.println("\n--- Status da Produção ---");
                    if (vitrineProducao.isEmpty()) {
                        System.out.println("Nenhum item em produção.");
                    } else {
                        for (int i = 0; i < vitrineProducao.size(); i++) {
                            System.out.println(i + ". " + vitrineProducao.get(i));
                        }
                    }
                    break;

                case 3:
                    System.out.print("Digite o índice do item para assert: ");
                    int index = leitor.nextInt();
                    if (index >= 0 && index < vitrineProducao.size()) {
                        Produto selecionado = vitrineProducao.get(index);
                        if (selecionado.isAssado()) {
                            System.out.println("Este item já está assado e pronto para venda!");
                        } else {
                            selecionado.setAssado(true);
                            System.out.println("O " + selecionado.getNome() + " acabou de sair do forno! Cheiro de pão fresco no ar.");
                        }
                    } else {
                        System.out.println("Item não encontrado na produção.");
                    }
                    break;
                default:
                    throw new IllegalStateException("Unexpected value: " + opcao);
            }

        } while (opcao != 4);
        leitor.close();
        System.out.println("Sistema da padaria desligado.");

    }
}

package Main;

public class Produto {
    private String nome;
    private String categoria; // Ex: Pão, Doce, Salgado
    private boolean assado;

    public Produto(String nome, String categoria) {
        this.nome = nome;
        this.categoria = categoria;
        this.assado = false; // Todo produto começa na vitrine de produção
    }

    // Getters
    public String getNome() { return nome; }
    public String getCategoria() { return categoria; }
    public boolean isAssado() { return assado; }

    // Setter para atualizar quando sair do forno
    public void setAssado(boolean assado) {
        this.assado = assado;
    }

    @Override
    public String toString() {
        String status = assado ? "[QUENTINHO]" : "[NO FORNO]";
        return status + " " + nome + " (" + categoria + ")";
    }
}

package Main;

import java.util.ArrayList;

public class Homologação {
    public static void main(String[] args) {
        ArrayList<Produto> estoqueTeste = new ArrayList<>();

        // Simulação de produção
        estoqueTeste.add(new Produto("Pão Francês", "Pães"));
        estoqueTeste.add(new Produto("Croissant de Chocolate", "Doces"));
        estoqueTeste.add(new Produto("Coxinha", "Salgados"));

        System.out.println("Verificando itens na fila de espera...");
        if (estoqueTeste.size() == 3) {
            System.out.println("Sucesso: 3 massas aguardando o forno.");
        }

        // Testando a lógica de "Assar"
        Produto teste = estoqueTeste.get(0);
        System.out.println("Status inicial: " + teste);
        teste.setAssado(true);

        if (teste.isAssado()) {
            System.out.println("Sucesso: O status do " + teste.getNome() + " mudou para assado.");
            System.out.println("Status final: " + teste);
        }
    }
}
