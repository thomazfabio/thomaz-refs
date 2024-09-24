Para autenticar o seu servidor Ubuntu com o GitHub, o método mais seguro e recomendado é usar **chaves SSH** para realizar a autenticação sem a necessidade de inserir sua senha sempre que você interagir com seus repositórios no GitHub.

Aqui está o passo a passo para configurar a autenticação via SSH:

### 1. **Gerar uma Chave SSH no Servidor**
Se ainda não tem uma chave SSH no seu servidor Ubuntu, você pode gerar uma nova chave:

```bash
ssh-keygen -t ed25519 -C "seu_email@example.com"
```

- **`-t ed25519`** especifica o tipo de chave. Você também pode usar `rsa` se preferir.
- **`-C`** é o comentário associado à chave (geralmente seu e-mail do GitHub).

Ao ser solicitado para salvar a chave, pressione **Enter** para aceitar o caminho padrão (`/home/usuário/.ssh/id_ed25519`).

### 2. **Adicionar a Chave SSH ao ssh-agent**
Se o **ssh-agent** não estiver em execução, inicie-o:

```bash
eval "$(ssh-agent -s)"
```

Agora adicione sua chave privada ao agente SSH:

```bash
ssh-add ~/.ssh/id_ed25519
```

### 3. **Copiar a Chave Pública**
Você precisará da chave pública para adicionar ao GitHub. Para copiar a chave pública, use o seguinte comando:

```bash
cat ~/.ssh/id_ed25519.pub
```

Isso exibirá a chave pública no terminal. Copie o texto inteiro.

### 4. **Adicionar a Chave SSH ao GitHub**
1. Entre na sua conta do **GitHub**.
2. No canto superior direito, clique na sua foto de perfil e vá para **Settings**.
3. No menu da esquerda, clique em **SSH and GPG keys**.
4. Clique no botão **New SSH key**.
5. Dê um nome à sua chave (por exemplo, "Contabo Server") e cole a chave pública copiada no campo de chave.
6. Clique em **Add SSH key**.

### 5. **Configurar o Git para Usar o SSH**
Agora, para garantir que o Git use a autenticação SSH ao interagir com o GitHub, configure o repositório ou o Git globalmente para usar a URL SSH em vez da URL HTTPS.

Para um repositório específico:

```bash
git remote set-url origin git@github.com:usuario/nome-do-repositorio.git
```

Ou, para clonar repositórios diretamente usando SSH:

```bash
git clone git@github.com:usuario/nome-do-repositorio.git
```

### 6. **Testar a Conexão**
Para testar se tudo está funcionando corretamente, execute:

```bash
ssh -T git@github.com
```

Se tudo estiver configurado corretamente, você verá uma mensagem como:

```bash
Hi nome_do_usuario! You've successfully authenticated, but GitHub does not provide shell access.
```

Isso significa que sua autenticação SSH está funcionando corretamente.

### Conclusão:
Agora você configurou com sucesso o seu servidor Ubuntu para autenticar com o GitHub usando chaves SSH. Isso permitirá que você faça `git pull`, `git push` e outras operações sem precisar digitar a senha a cada vez.