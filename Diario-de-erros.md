## 20/11/2026 - `1s`: command not found
- **O que eu estava tentando fazer:** listar os arquivos da pasta
- **O que aconteceu:** o terminal respondeu "command not found"
- **Causa:** digitei `1s` (número 1) no lugar de `ls` (letra L)
- **Como resolvi:** Perguntei ao claude o motivo do comando estar dando errado e ele apontou o erro de digitação ao colocar o número 1 no lugar da letra L
- **O que aprendi:** "command not found" quase sempre é erro de digitação, conferir melhor o comando letra por letra antes de ver o motivo do erro
- **Onde pesquisei:** conversa com o Claude


## 20/11/2026 - `apt update`: Permission denied
- **O que eu estava tentando fazer:** Estava tentando ver as atualizações disponíveis e atualizar o sistema, porém agora sei que o `update` somente atualiza a lista.
- **O que aconteceu:** o terminal respondeu "Não pude abrir ficheiro de tranca /var/lib/apt/lists/lock - open (13:  Permission denied)"
- **Causa:** ao colocar apenas `apt update` sem colocar anteriormente o `sudo`, o comando não funcionou, pois o `apt` altera os arquivos do sistema, e o comando `sudo` executa os comandos com privilégios de administrador temporariamente. Isso mostrou que o problema era apenas falta de permissão, pois, se tivesse outra operação de dados ocorrendo, apesar da permissão de administrador, não seria possível instalar algo por conta das travas do sistema que impedem duas operações de pacotes de forma simultânea. 
- **Como resolvi:** Eu rodei de novo o comando e pesquisei no google o erro que estava me aparecendo. Após ver o resumo feito pela a ia, vi que o problema mais comum é o sudo, então bastou colocar um `sudo` antes do comando para a atualização começar, pois, se tivesse outro processo usando `apt`, apesar da permissão de administrador, não seria possível instalar algo por conta das travas do sistema que impedem duas operações de pacotes simultaneamente.
- **O que aprendi:** Por meio do resumo da ia do google entendi que o `apt` é algo que precisa de autorização do administrador para alterar os arquivos do sistema e também onde aprendi que o `sudo` da essa permissão temporária de administrador. Também aprendi que `Permission denied` diz que meu usuário não tinha permissão de administrador, o que é bem diferente de já ter outro processo em atividade, além de que apagar o arquivo `lock` para forçar a instalação de algum arquivo não é bom, pois é muito perigoso ficar sem esse arquivo e a trava só vai impedir alguma alteração de pacotes se já houver algum processo em atividade. 
- **Descoberta:** `apt upgrade` falha em `/var/lib/dpkg/lock-frontend`. Minha teoria inicial era que o `apt upgrade` fazia a busca dos arquivos por fora (por isso é frontend) e que o update fazia a instalação desses arquivos de atualização que o upgrade buscava, mas na realidade descobri que estava completamente errado, o comando `apt update` é quem consulta os repositórios e altera a lista de atualizações disponíveis, enquanto com o comando `apt upgrade` instalamos essas atualizações. O `apt` baixa os pacotes da internet, e depois o `dpkg` pega esses arquivos e faz as alterações no sistema, já o `dpkg lock-frontend` é o bloqueio que impede mais de um `dpkg` funcionar ao mesmo tempo. O `update` falha em `/var/lib/apt/lists/` por não ter permissão de administrador, e o upgrade falha em `/var/lib/dpkg/` pelo mesmo motivo, também não tinha a permissão de administrador. Nos dois casos o comando `sudo` resolveu o problema. 
- **Onde pesquisei:** Conversei com o Claude, consultei o comando `man apt` e pesquisei no google


## 25/11/2026 - `ls`: achei que `ls` executava ações em vez de só listar
- **O que eu estava tentando fazer:** Estava tentando prever o que aconteceria ao testar o comando `ls /var/lib/apt/lists/`
- **O que aconteceu:** o comando listou os arquivos que existiam na pasta, eu pensei que iria fazer algo similar a função do `apt update`, porém, confundi completamente a função do comando, uma vez que o `ls` não toma ações sobre os arquivos
- **Causa:** achei inicialmente que o ls fosse executar alguma ação por conta do `apt` incluso no argumento, eu confundi com o comando `apt update` que a minha cabeça associou 
- **Como resolvi:** ao colocar no terminal o comando `ls /var/lib/apt/lists/`, vi que não ocorreu nenhuma alteração como tinha pensado inicialmente, percebi que apenas me foi mostrado tudo que estava inserido na pasta pesquisada, logo entendi que o comando não executava ações e sim que ele listava os arquivos da pasta desejada
- **O que aprendi:** Aprendi que o comando `ls` nunca altera alguma pasta ou arquivo, ela apenas mostra em lista os arquivos dentro da pasta desejada. Também entendi que os comandos `apt` tomam ações sobre os pacotes que estão na pasta `lists`, enquanto a função dessa pasta é guardar o catálogo de atualizações
- **Onde pesquisei:** Conversei com o Claude e analisei o que me apareceu para entender
