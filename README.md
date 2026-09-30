# Portal PET-Saude — Hub de Acesso Unificado

Portal de entrada unificado dos sistemas integrados de saude coletiva
desenvolvidos pelo PET-Saude Informacao e Saude Digital (UFPI / Picos-PI).

## Sistemas disponibilizados

| Sistema      | Descricao                                            | URL de producao                      |
|--------------|------------------------------------------------------|--------------------------------------|
| Clara        | Assistente inteligente — estoque, PCDTs e IA clinica | https://clara.petsaudepicos.tech     |
| CadastraPET  | Mapeamento territorial e gestao academica            | https://cadastrapet.petsaudepicos.tech |

## Estrutura do projeto

```
Portal-PET-Saude/
├── assets/             # Imagens e logos institucionais
│   ├── ASSETS.md       # Instrucoes sobre quais arquivos colocar aqui
│   ├── logo_pet_bg.png
│   ├── logo_clara.png
│   ├── logo-ufpi-bg.png
│   ├── logo-secretaria.png
│   └── logo_cadastrapet.png  (PENDENTE — adicionar antes do deploy final)
├── nginx/
│   └── default.conf    # Configuracao Nginx do servidor de producao
├── index.html          # Pagina principal do portal (pagina unica)
├── style.css           # Estilos auxiliares (se houver)
├── Dockerfile          # Imagem Nginx Alpine com os arquivos estaticos
├── docker-compose.yml  # Orquestracao do container do portal
└── README.md
```

## Como rodar localmente

```bash
# Servir direto pelo browser (sem docker)
# Abra index.html no navegador

# Ou com Docker
docker compose up -d --build
# Acesse: http://localhost:8080
```

## Deploy no servidor (Hostinger VPS)

Ver secao "Arquitetura de producao" abaixo.

### 1. Clonar o repositorio no servidor

```bash
cd /var/www
git clone https://github.com/outbreakufpi/Portal-PET-Saude.git
cd Portal-PET-Saude
```

### 2. Subir o container

```bash
docker compose up -d --build
```

### 3. Atualizar apos mudancas

```bash
cd /var/www/Portal-PET-Saude
git pull origin main
docker compose up -d --build
```

## Arquitetura de producao

```
Internet
    |
    v
Nginx (host) — porta 80/443
    |
    ├── petsaudepicos.tech  (dominio raiz)
    |       └── proxy_pass -> portal container (porta interna 8080)
    |
    └── clara.petsaudepicos.tech  (subdominio)
            └── proxy_pass -> clara container (porta interna 3000)
```

O arquivo `nginx/default.conf` contem a configuracao completa para
o servidor de producao. Ele deve ser copiado para `/etc/nginx/conf.d/`
na VPS e o Nginx reiniciado apos qualquer alteracao.

## Assets — imagens pendentes

Ao receber o arquivo PNG do icone do CadastraPET:

1. Salve como `assets/logo_cadastrapet.png`
2. No `index.html`, substitua a URL `lh3.googleusercontent.com/...` do
   card CadastraPET por `assets/logo_cadastrapet.png`
3. Faca commit e atualize no servidor com `git pull` + `docker compose up -d --build`

## Vinculo com o repositorio Clara

Este repositorio e independente do repositorio principal do Sistema Clara.
Ambos sao gerenciados separadamente e se comunicam apenas via URL publica.

---

PET-Saude Informacao e Saude Digital — UFPI / Picos-PI — 2026
