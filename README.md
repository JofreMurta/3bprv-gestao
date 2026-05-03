# 3º BPRv — P/3 — Sistema de Gestão de Atividades

Sistema web para controle de prazos, atividades e documentos entre o Batalhão e as quatro Companhias do 3º Batalhão de Polícia Rodoviária.

---

## Funcionalidades

- **Três módulos**: Operações, Estatística e Gabinete de Treinamento
- **Controle de prazos** com indicação visual por cores (verde / amarelo / vermelho)
- **Ciência automática** ao acessar o sistema
- **Anexo de documentos**: documento de referência pelo Batalhão + resposta por Companhia
- **Justificativa obrigatória** quando o prazo vence sem cumprimento
- **Relatório exportável** em Excel (.xlsx) e PDF (.html para impressão)
- **Acesso por senha** por OPM (sem dependência de domínio institucional)
- **Atividades coletivas e individuais**

---

## Perfis de Acesso

| OPM | Permissões |
|---|---|
| **Batalhão** | Criar atividades, visualizar todas as OPMs, anexar doc. referência, extrair relatórios |
| **Companhias** | Visualizar próprias atividades, marcar cumprimento, anexar resposta, justificar atrasos |

---

## Configuração Firebase (obrigatória para uso em produção)

### 1. Criar projeto no Firebase

1. Acesse [console.firebase.google.com](https://console.firebase.google.com)
2. Clique em **Adicionar projeto**
3. Dê um nome (ex: `3bprv-gestao`) e confirme

### 2. Ativar os serviços necessários

No menu lateral do console Firebase:

- **Authentication** → Método de login → **E-mail/senha** → Ativar *(não será usado diretamente, mas é necessário para as regras)*
- **Firestore Database** → Criar banco de dados → Modo **produção**
- **Storage** → Começar → Modo **produção**

### 3. Registrar o aplicativo web

1. No console do projeto → ícone `</>` (Web)
2. Registre o app com um apelido (ex: `3bprv-web`)
3. **Copie as credenciais** exibidas (`firebaseConfig`)

### 4. Inserir as credenciais no arquivo

Abra o arquivo `3bprv_gestao.html` e localize o trecho:

```javascript
const firebaseConfig = {
  apiKey:            "COLE_SUA_API_KEY",
  authDomain:        "COLE_SEU_AUTH_DOMAIN",
  projectId:         "COLE_SEU_PROJECT_ID",
  storageBucket:     "COLE_SEU_STORAGE_BUCKET",
  messagingSenderId: "COLE_SEU_SENDER_ID",
  appId:             "COLE_SEU_APP_ID"
};
```

Substitua cada valor pelo correspondente das suas credenciais Firebase.

### 5. Definir as senhas das OPMs

No mesmo arquivo, localize:

```javascript
const SENHAS = {
  "Batalhão": "senha_batalhao",
  "1ª Cia":   "senha_1cia",
  "2ª Cia":   "senha_2cia",
  "3ª Cia":   "senha_3cia",
  "4ª Cia":   "senha_4cia"
};
```

Substitua por senhas seguras e comunique cada OPM a sua respectiva senha.

> ⚠️ **Importante:** não publique as senhas no repositório GitHub. Use senhas fortes e diferentes para cada OPM.

### 6. Aplicar regras de segurança no Firestore

No console Firebase → Firestore → **Regras**, cole o conteúdo do arquivo `firestore.rules` deste repositório e publique.

### 7. Aplicar regras de segurança no Storage

No console Firebase → Storage → **Regras**, cole o conteúdo do arquivo `storage.rules` e publique.

---

## Hospedagem

### Opção A — GitHub Pages (recomendada, gratuita)

1. Faça upload do arquivo `3bprv_gestao.html` para este repositório
2. No GitHub → **Settings** → **Pages**
3. Selecione branch `main` e pasta `/root`
4. O sistema ficará disponível em `https://SEU_USUARIO.github.io/NOME_DO_REPOSITORIO/3bprv_gestao.html`

### Opção B — Firebase Hosting (alternativa gratuita)

```bash
npm install -g firebase-tools
firebase login
firebase init hosting
firebase deploy
```

### Opção C — Uso local

Abra o arquivo `3bprv_gestao.html` diretamente no navegador. Os dados serão gravados no Firebase normalmente, desde que haja conexão com a internet.

---

## Estrutura do Repositório

```
3bprv-gestao/
├── 3bprv_gestao.html   # Aplicação principal (único arquivo)
├── firestore.rules     # Regras de segurança do banco de dados
├── storage.rules       # Regras de segurança dos arquivos
└── README.md           # Este arquivo
```

---

## Modo Demonstração

Se o Firebase não estiver configurado (credenciais ainda com `COLE_...`), o sistema abre automaticamente em **modo demonstração** com dados simulados. Use o seletor no cabeçalho para alternar entre os perfis de OPM.

---

## Suporte

Sistema desenvolvido para uso interno do **3º Batalhão de Polícia Rodoviária — P/3**.
