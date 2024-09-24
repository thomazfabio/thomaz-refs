Para criar um usuário no servidor com permissões de escrita e gravação apenas em seu próprio diretório, siga os passos abaixo:

### 1. **Criar o Usuário**
Use o comando `adduser` para criar um novo usuário e configurar sua senha:

```bash
sudo adduser nome_do_usuario
```

Isso cria o diretório home do usuário em `/home/nome_do_usuario` e também configura uma senha para o usuário.

### 2. **Definir Permissões no Diretório Home**
Por padrão, o diretório home do usuário será `/home/nome_do_usuario`. Para garantir que o usuário tenha permissão de escrita e leitura apenas nesse diretório, ajuste as permissões da seguinte forma:

```bash
sudo chmod 700 /home/nome_do_usuario
```

Isso garante que apenas o usuário tenha acesso total (leitura, gravação e execução) ao seu próprio diretório. Outros usuários, incluindo o `root`, poderão acessar o diretório, mas outros usuários normais não poderão.

### 3. **Remover Acesso a Outras Pastas**
Por padrão, um novo usuário não tem permissões para alterar ou modificar arquivos em outros diretórios do sistema (como `/etc`, `/var`, etc.). Para garantir que o usuário não tenha permissões fora do seu diretório home, verifique as permissões dos diretórios principais do sistema:

```bash
ls -ld / /home /var /etc
```

Esses diretórios devem ter permissões restritas para que apenas o `root` ou usuários com permissões adequadas possam fazer alterações.

### 4. **Atribuir Grupo Específico (Opcional)**
Você pode criar um grupo específico para esse usuário, caso queira definir permissões mais detalhadas para diretórios específicos. Por exemplo:

```bash
sudo groupadd grupo_especifico
sudo usermod -aG grupo_especifico nome_do_usuario
```

Isso adiciona o usuário ao grupo `grupo_especifico`. Você pode então aplicar permissões específicas de grupo em diretórios, se necessário.

### 5. **Testar as Permissões**
Faça login com o novo usuário para testar as permissões:

```bash
su - nome_do_usuario
```

Verifique se o usuário pode escrever no próprio diretório home e tente acessar outros diretórios para garantir que as permissões estão corretas.

### Conclusão

- **Comando para criar o usuário**: `sudo adduser nome_do_usuario`
- **Permissões no diretório home**: `sudo chmod 700 /home/nome_do_usuario`
- **Testar permissões**: `su - nome_do_usuario`

Com isso, o novo usuário poderá ler, gravar e executar apenas dentro de seu próprio diretório, sem afetar outras áreas do sistema.