# Livia Bitencoutt — versão para hospedagem independente

## Arquivos
- `index.html`: página principal, com CSS embutido e imagens em WebP Base64.
- `privacidade.html`: página inicial de privacidade vinculada ao rodapé.
- `AUDITORIA.md`: achados, correções realizadas e itens que dependem de confirmação.

## Publicação
1. Envie os dois arquivos HTML para a raiz do diretório público da hospedagem (por exemplo, `public/` ou `public_html/`).
2. Abra `index.html` no domínio final e teste os links do menu, menu móvel, imagens e os três CTAs do WhatsApp.
3. Confirme com a cliente que o número `+55 51 98515-0661` continua correto.
4. O domínio `https://liviabitencourt.pages.dev/` já está configurado no canonical e em `og:url`. Configure uma imagem social `og:image` somente depois de criar uma imagem própria e publicá-la em URL pública.
5. Revise a política de privacidade com base nas práticas efetivas da hospedagem e em qualquer ferramenta adicionada no futuro.
6. O aviso 18+ pede confirmação declaratória e lembra que não é verificação documental. Ele é armazenado apenas durante a sessão do navegador.

## Dependências externas remanescentes
- Nenhuma biblioteca JavaScript externa nem Google Fonts. A tipografia utiliza fontes do sistema.
- WhatsApp é um destino externo dos links de contato.

Não há build step, npm, Astro, runtime da Kleap, imagens em caminhos locais ou chamadas a endpoints da Kleap.
