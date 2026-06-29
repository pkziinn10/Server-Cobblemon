# Servidor Minecraft Modificado (Fabric 1.21.1) via Docker

Este projeto contém a configuração completa para rodar um servidor de Minecraft modificado de forma segura, isolada e com salvamento automático usando **Docker**.

## 📁 Estrutura de Pastas

Ao rodar o servidor, todas as suas informações vitais ficam salvas fisicamente nas pastas locais. Isso garante que nenhum progresso seja perdido caso o servidor reinicie:

- `data/`: É o coração do servidor. Aqui ficam guardados o seu mundo (mapa), o inventário dos jogadores, os dados de pokémons e os arquivos vitais como `ops.json` (permissões).
- `mods/`: Todos os arquivos `.jar` (mods) que o servidor deve carregar precisam estar dentro desta pasta. Nós estamos usando o modpack do **Cobblemon** e várias outras dependências.
- `config/`: Arquivos de configuração específicos dos mods.

## 🚀 Como Iniciar e Parar o Servidor

Você não precisa abrir terminais do Minecraft ou rodar scripts complexos. Tudo é feito via Docker:

### Ligar o servidor (em segundo plano)
```bash
docker compose up -d
```
> *Nota: O parâmetro `-d` faz o servidor rodar silenciosamente em segundo plano, deixando o seu terminal livre para uso.*

### Desligar o servidor (com segurança)
Para garantir que o mundo seja salvo corretamente, **nunca** feche o processo abruptamente. Use:
```bash
docker compose stop
```
> *Use `docker compose down` apenas se quiser desligar e também remover o container virtual (o seu mapa na pasta `data` não será apagado).*

### Acompanhar os Logs (Terminal do jogo)
Para ver o console do servidor em tempo real (como o mapa carregando, jogadores entrando ou erros):
```bash
docker compose logs -f
```
*(Pressione `CTRL + C` para sair da tela de logs. O servidor continuará ligado).*

## ⚙️ Configurações e Comandos Úteis

### Dar permissão de Administrador (OP)
Se algum jogador precisar quebrar blocos no Spawn ou usar comandos, você pode dar OP para ele direto do terminal do seu PC sem precisar estar dentro do jogo:
```bash
docker exec minecraft rcon-cli op NomeDoJogador
```

### Configurações Atuais (`docker-compose.yml`)
- **Versão:** Fabric 1.21.1
- **Memória RAM:** 6GB alocados para aguentar +100 mods suavemente.
- **Conta Original:** A verificação de conta original está **LIGADA** (`ONLINE_MODE: "TRUE"`). Jogadores precisam estar logados pelo launcher oficial (ou PrismLauncher autenticado) para entrar.
