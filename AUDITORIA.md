# Auditoria técnica — Livia Bitencoutt

## Escopo e limitações
Auditoria estática do HTML fornecido e preparação de uma versão independente para hospedagem estática. Foram inspecionados metadados, navegação, scripts, dependências, imagens, referências locais e links. Não foi possível confirmar o comportamento em navegadores reais, métricas Lighthouse/Core Web Vitals, respostas HTTP do domínio final ou disponibilidade real do WhatsApp a partir deste arquivo isolado.

## Principais achados na versão de origem

### Críticos para publicação independente
1. **Acoplamento ao ambiente de preview Kleap/Astro.** O documento continha runtime Astro em `data:` e scripts de preview/edição (`kleap-shim`, tagger React, seletor de componentes e roteamento do iframe). Esses recursos não fazem parte do site público e não são necessários para servir HTML estático.
2. **URLs e metadados de publicação apontavam para a Kleap.** Canonical e Open Graph usavam `prompt-mestre-site-de-livia.kleap.io`; a imagem social era gerada por `kleap.co`; o `og:site_name` e o JSON-LD identificavam `kleap-app-117956`. Isso seria incorreto após a migração.
3. **Rotas internas não eram páginas autônomas.** Links `/servicos`, `/sobre` e `/contato` não correspondiam a páginas fornecidas no arquivo HTML. Em hospedagem estática simples, poderiam resultar em 404.
4. **O menu móvel dependia de um script de preview.** O script Kleap inseria o controle do menu. Sem ele, a navegação mobile ficaria sem controle visível.
5. **Favicons e manifesto referenciavam arquivos locais não incluídos no HTML.** Os caminhos `/favicon.svg`, `/favicon-32.png`, `/apple-touch-icon.png` e `/site.webmanifest` poderiam resultar em 404.

### Melhorias de qualidade
6. **Imagens embutidas em Base64.** Isso elimina dependência de caminhos de imagem externos, mas mantém os bytes das imagens dentro do HTML e impede cache independente das imagens. Para este arquivo, foi preservado para facilitar publicação com poucos arquivos.
7. **Tipografia carregada do Google Fonts.** É uma dependência externa não relacionada à Kleap. O layout mantém fallback de fontes, mas uma chamada externa pode ocorrer. Hospedar fontes localmente ou usar fontes do sistema elimina essa chamada.
8. **Marca inconsistente no logotipo.** O cabeçalho trazia “BITENCOURT”, enquanto o restante da página usa “Bitencoutt”. O cabeçalho foi padronizado para “BITENCOUTT”, conforme o briefing recebido.
9. **Texto de serviço com grafia inadequada.** “Acompanhia personalizada” foi corrigido para “Companhia personalizada”.
10. **Metadados sociais sem domínio final válido.** A versão independente mantém título, descrição e nome do site, mas não inventa canonical, `og:url` ou `og:image` até que o domínio e uma imagem social pública sejam definidos.

## Correções aplicadas
- Removidos scripts de runtime Astro e scripts de edição/preview Kleap, além do script de menu gerado pela plataforma.
- Removidos atributos e referências específicas de Kleap e rotas de preview.
- Removidos canonical, URLs sociais, imagem OG e JSON-LD que apontavam para o domínio/plataforma de origem.
- Convertidos links internos para âncoras da própria página (`#inicio`, `#sobre`, `#servicos`, `#contato`).
- Criado menu móvel próprio, com JavaScript nativo, `aria-controls`, `aria-expanded`, fechamento ao navegar e suporte à tecla Escape.
- Criado `privacidade.html` e atualizado o link do rodapé para esse arquivo.
- Mantidas as imagens WebP embutidas; adicionados `decoding="async"` e carregamento lazy para a imagem secundária.
- Adicionado `target="_blank"` com `rel="noopener noreferrer"` nos links de WhatsApp.
- Removidos caminhos de favicon/manifesto que não estavam incluídos no material fornecido.
- Padronizada a grafia da marca e corrigido “Companhia personalizada”.
- Mantidos CSS e identidade visual existentes, incluindo a paleta `#160D0E`, `#D6AD75`, `#722F3B` e `#F2E5D7`.

## Validações estáticas realizadas
- HTML principal não contém referências a `kleap.io`, `kleap.co`, `data-kleap`, `kleap-shim`, eventos `astro:page-load` nem rotas antigas `/servicos`, `/sobre`, `/contato` ou `/privacidade`.
- Links de âncora internos apontam para IDs existentes.
- Não há `src` ou `href` local absoluto começando com `/` que dependa de arquivos não entregues.
- O JavaScript próprio do menu passou pela verificação sintática de Node.js.
- A página principal e a página de privacidade são HTML estático; não exigem processo de build.

## Pendências antes da publicação
1. **Confirmar número de WhatsApp** `+55 51 98515-0661` com a cliente.
2. **Definir domínio definitivo** e adicionar canonical/OG absolutos e imagem social pública.
3. **Revisar a política de privacidade.** O texto fornecido é inicial; deve refletir o provedor de hospedagem, os serviços externos e a prática real do site.
4. **Decidir sobre Google Fonts.** Se a prioridade for eliminar qualquer dependência externa, usar fontes de sistema ou hospedar fontes licenciadas localmente.
5. **Testar após upload** em desktop e celular, incluindo navegação, menu, WhatsApp, política de privacidade e compartilhamento em redes sociais.
6. **Verificar conteúdo e direitos de uso das imagens** antes de publicar.

## Recomendação
A versão preparada é apropriada como base para hospedagem estática independente. A migração de código foi realizada, mas o aceite final deve ocorrer após teste no domínio de produção e confirmação dos itens pendentes acima.


## Atualização solicitada — identidade editorial e aviso 18+

- Configurado o domínio canônico `https://liviabitencourt.pages.dev/` e `og:url` para esse endereço.
- Adicionado aviso de entrada para maiores de 18 anos, com confirmação declaratória, opção de saída, foco acessível e bloqueio de rolagem enquanto o aviso está aberto. A confirmação dura somente a sessão do navegador; não é verificação real de idade.
- Removidas as requisições do Google Fonts e os metadados de transição do Astro. A tipografia usa fontes do sistema, reduzindo requisições externas e sinais de template.
- Reescritos textos genéricos para linguagem mais direta e específica; corrigida a ocorrência de `Bitencout` sem o segundo `t`.
- Atualizada a política de privacidade para refletir a ausência de Google Fonts.
- O domínio é um Pages de Cloudflare, mas a publicação real não foi executada por esta alteração local. Testar o domínio após fazer upload dos arquivos.
- A confirmação 18+ é apenas declaratória; não deve ser descrita como mecanismo de verificação ou garantia de conformidade legal.
