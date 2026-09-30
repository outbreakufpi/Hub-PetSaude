# Pasta de Assets do Portal

Coloque aqui os arquivos de imagem antes de subir para o servidor.
Todos os arquivos devem estar nesta pasta (assets/).

## Imagens esperadas

| Arquivo               | Uso no portal                          | Status   |
|-----------------------|----------------------------------------|----------|
| logo_pet_bg.png       | Favicon e logo do header (PET-Saude)   | Presente |
| logo_clara.png        | Card do Sistema Clara                  | Presente |
| logo-ufpi-bg.png      | Rodape - Instituicao UFPI              | Presente |
| logo-secretaria.png   | Rodape - Secretaria de Saude de Picos  | Presente |
| logo_cadastrapet.png  | Card do Sistema CadastraPET            | PENDENTE |

## Como atualizar as imagens no HTML

Apos adicionar o arquivo PNG nesta pasta, edite o index.html e
substitua a URL do src da imagem correspondente por:

  src="assets/nome-do-arquivo.png"

## Convencao de nomes

- Letras minusculas
- Sem espacos (use hifen ou underscore)
- Formato: PNG ou SVG (preferencia PNG com fundo transparente)
- Tamanho recomendado para logos de card: 128x128 px
- Tamanho recomendado para logos de rodape: 80x80 px
