Descrição do Projeto
Este projeto consiste em uma aplicação Java que gerencia músicas e podcasts, registrando reproduções, curtidas e classificações. Ele também identifica e destaca conteúdos populares com base em suas classificações.

Estrutura do Projeto
O projeto está dividido em três pacotes principais:

modelos: Contém as classes base e as especializadas para áudio, música e podcast.
principal: Contém a classe principal que executa a aplicação.
Classes
Classe Audio
Esta classe é a base para representar um áudio. Ela possui atributos e métodos básicos que são comuns para qualquer tipo de áudio.

java
Copiar código
package modelos;

public class Audio {
    private String Titulo;
    private int totalReproducoes;
    private int totalCurtidas;
    private int classificacao;

    public void setTitulo(String titulo) {
        Titulo = titulo;
    }

    public String getTitulo() {
        return Titulo;
    }

    public int getTotalReproducoes() {
        return totalReproducoes;
    }

    public int getTotalCurtidas() {
        return totalCurtidas;
    }

    public int getClassificacao() {
        return classificacao;
    }

    public void curte() {
        this.totalCurtidas++;
    }

    public void reproduzir() {
        this.totalReproducoes++;
    }
}
Classe Musica
Extende a classe Audio e adiciona atributos específicos para músicas, como álbum, cantor e gênero. Sobrescreve o método getClassificacao para determinar a classificação baseada em reproduções.

java
Copiar código
package modelos;

public class Musica extends Audio {
    private String album;
    private String cantor;
    private String genero;

    public String getAlbum() {
        return album;
    }

    public void setAlbum(String album) {
        this.album = album;
    }

    public String getCantor() {
        return cantor;
    }

    public void setCantor(String cantor) {
        this.cantor = cantor;
    }

    public String getGenero() {
        return genero;
    }

    public void setGenero(String genero) {
        this.genero = genero;
    }

    @Override
    public int getClassificacao() {
        if (this.getTotalReproducoes() > 2000) {
            return 10;
        } else {
            return 7;
        }
    }
}
Classe Podcast
Extende a classe Audio e adiciona atributos específicos para podcasts, como apresentador e descrição. Sobrescreve o método getClassificacao para determinar a classificação baseada em curtidas.

java
Copiar código
package modelos;

public class Podcast extends Audio {
    private String apresentador;
    private String descricao;

    public String getApresentador() {
        return apresentador;
    }

    public void setApresentador(String apresentador) {
        this.apresentador = apresentador;
    }

    public String getDescricao() {
        return descricao;
    }

    public void setDescricao(String descricao) {
        this.descricao = descricao;
    }

    @Override
    public int getClassificacao() {
        if (this.getTotalCurtidas() > 500) {
            return 10;
        } else {
            return 8;
        }
    }
}
Classe MinhasPreferidas
Esta classe inclui métodos para adicionar um áudio à lista de preferidos, com base na classificação.

java
Copiar código
package modelos;

public class MinhasPreferidas {

    public void inclui(Audio audio) {
        if (audio.getClassificacao() >= 9) {
            System.out.println(audio.getTitulo() + " é considerado sucesso absoluto e preferido por todos.");
        } else {
            System.out.println(audio.getTitulo() + " também é um dos que todo mundo está curtindo.");
        }
    }
}
Classe Principal
A classe principal onde a aplicação é executada. Instancia objetos de Musica e Podcast, simula reproduções e curtidas, e inclui os áudios na lista de preferidos.

java
Copiar código
package principal;

import modelos.MinhasPreferidas;
import modelos.Musica;
import modelos.Podcast;

public class Principal {
    public static void main(String[] args) {
        Musica minhaMusica = new Musica();
        minhaMusica.setTitulo("Forever");
        minhaMusica.setCantor("Kiss");

        for (int i = 0; i < 1000; i++) {
            minhaMusica.reproduzir();
        }

        for (int i = 0; i < 50; i++) {
            minhaMusica.curte();
        }

        Podcast meuPodcast = new Podcast();
        meuPodcast.setTitulo("BolhaDev");
        meuPodcast.setApresentador("Marquinhos");

        for (int i = 0; i < 5000; i++) {
            meuPodcast.reproduzir();
        }

        for (int i = 0; i < 1000; i++) {
            meuPodcast.curte();
        }

        MinhasPreferidas preferidas = new MinhasPreferidas();
        preferidas.inclui(meuPodcast);
        preferidas.inclui(minhaMusica);
    }
}
Como Executar
Certifique-se de ter o JDK instalado em sua máquina.
Compile os arquivos .java com o comando javac.
Execute a classe principal Principal para ver o resultado.
bash
Copiar código
javac modelos/*.java principal/Principal.java
java principal.Principal
Contribuição
Contribuição ao curso da Alura sobre orientação a objetos.

Licença
Este projeto está licenciado pelos cursos da Alura.
