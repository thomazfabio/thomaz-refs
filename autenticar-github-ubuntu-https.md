Você pode autenticar o seu servidor Ubuntu com o GitHub via HTTPS. No entanto, a autenticação via HTTPS geralmente requer o uso de **Tokens de Acesso Pessoal (PAT)** em vez de sua senha de GitHub.

Aqui está o passo a passo para autenticar via HTTPS com um **Token de Acesso Pessoal**:

### 1. **Gerar um Token de Acesso Pessoal no GitHub**

1. Acesse o GitHub e faça login na sua conta.
2. No canto superior direito, clique no ícone de perfil e vá para **Settings**.
3. No menu da esquerda, clique em **Developer settings**.
4. No submenu, clique em **Personal access tokens** e depois em **Tokens (classic)**.
5. Clique em **Generate new token** (ou **Generate new token (classic)**).
6. Dê um nome ao token, defina o prazo de validade e selecione os escopos adequados (como `repo` para ter acesso total aos repositórios).
7. Clique em **Generate token** no final.

**Importante**: Copie o token gerado. Ele será exibido apenas uma vez.

### 2. **Clonar o Repositório via HTTPS**
Agora você pode clonar o repositório GitHub no seu servidor Ubuntu via HTTPS, mas, em vez de usar a senha, você usará o token que acabou de gerar.

Ao clonar o repositório, use a URL HTTPS do GitHub. Por exemplo:

```bash
git clone https://github.com/usuario/nome-do-repositorio.git
```

### 3. **Autenticação com o Token**
Durante o processo de `git clone`, `git pull` ou `git push`, o GitHub solicitará credenciais.

- **Nome de usuário**: Digite seu nome de usuário do GitHub.
- **Senha**: Insira o **Token de Acesso Pessoal** gerado no GitHub em vez da sua senha.

### 4. **Salvar as Credenciais (Opcional)**
Para evitar que o GitHub solicite suas credenciais a cada vez que você fizer um `git pull` ou `git push`, você pode configurar o Git para armazenar as credenciais:

```bash
git config --global credential.helper store
```

Agora, ao fornecer o token uma vez, ele será salvo para uso futuro e você não precisará digitá-lo novamente.

### Exemplo Completo:

1. Gere o Token de Acesso Pessoal no GitHub.
2. Clone o repositório usando HTTPS:

    ```bash
    git clone https://github.com/usuario/nome-do-repositorio.git
    ```

3. Quando solicitado:
    - Nome de usuário: Seu nome de usuário GitHub.
    - Senha: O Token de Acesso Pessoal.

4. Se quiser salvar as credenciais, use:

    ```bash
    git config --global credential.helper store
    ```

### 5. **Alterar Repositório Existente para HTTPS**
Se você já clonou um repositório via SSH ou outra URL e deseja mudar para HTTPS:

```bash
git remote set-url origin https://github.com/usuario/nome-do-repositorio.git
```

### Conclusão:
Autenticar via HTTPS no GitHub é possível usando um **Token de Acesso Pessoal (PAT)** em vez de sua senha do GitHub. Isso é mais seguro e recomendável, pois o GitHub não aceita mais autenticações com senha via HTTPS desde agosto de 2021.