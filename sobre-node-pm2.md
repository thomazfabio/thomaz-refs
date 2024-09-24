Com seu script de inicialização `"start": "node ./bin/www"`, você pode configurar o `pm2` para iniciar a aplicação usando diretamente o caminho do arquivo `./bin/www`.

Aqui está o comando para iniciar a aplicação com `pm2`:

```bash
pm2 start ./bin/www --name "meu-app"
```

### Explicação:
- `pm2 start ./bin/www`: Inicia o servidor Node.js executando o arquivo `./bin/www`.
- `--name "meu-app"`: Define um nome personalizado para o processo gerenciado pelo `pm2`, neste caso, "meu-app". Isso facilita o gerenciamento de múltiplos processos mais tarde.

### Comando completo:
Se você deseja usar o script do `package.json`, pode rodar:

```bash
pm2 start npm --name "meu-app" -- start
```

### Passos extras:
Após iniciar com `pm2`, você pode usar esses comandos úteis:
- Verificar o status dos processos em execução:

  ```bash
  pm2 list
  ```

- Parar o processo:

  ```bash
  pm2 stop meu-app
  ```

- Remover o processo:

  ```bash
  pm2 delete meu-app
  ```

- Verificar os logs:

  ```bash
  pm2 logs meu-app
  ```

Isso vai garantir que seu script seja executado corretamente pelo `pm2`.