# AutoVitrine — XR21MOTORS

Conceito demonstrativo de montra digital automóvel, desenvolvido pela **KRONUS Soluções Digitais**.
Protótipo navegável de alta fidelidade, em português de Portugal.

> Conceito comercial/demonstrativo. Não existe parceria oficial entre a KRONUS e a XR21MOTORS.
> Os dados de viaturas (`isDemo: true`) e depoimentos (`demoReview: true`) são exemplificativos.

## Conteúdo do repositório

```
AutoVitrine XR21MOTORS.dc.html   protótipo completo (abre direto no browser)
support.js                       runtime do protótipo
assets/                          fotografias do stand e logótipo
ARQUITETURA.md                   mapeamento para Next.js + TypeScript + Tailwind
```

## Como abrir

Servir a pasta e abrir o ficheiro no browser:

```bash
npx serve .
# ou
python3 -m http.server 8000
```

Abrir depois `AutoVitrine XR21MOTORS.dc.html`.

## O que está implementado

- Home: hero, pesquisa de viaturas, destaques, catálogo, serviços, financiamento, retomas, processo de compra, sobre, avaliações, CTA final e contactos.
- Catálogo com filtros client-side (marca, preço, ano, combustível, caixa), ordenação, contador, skeleton de carregamento e empty state.
- Página individual por viatura: galeria com lightbox, contador e zoom; especificações; equipamento por categoria; card de conversão sticky; barra fixa de preço em mobile.
- Formulários de financiamento e retoma com validação client-side, limites de caracteres, consentimento explícito e estados de sucesso.
- Banner RGPD com consentimento por categoria (necessários / analítica / marketing) e páginas de Privacidade, Cookies e Termos.
- WhatsApp com mensagem pré-preenchida por viatura.

## Configuração

Os dados do negócio (nome, telefone, WhatsApp, email, morada, Instagram) estão centralizados no objeto `cfg`, no topo da classe de lógica. `DEMO_MODE` está ativo: os formulários validam e simulam sucesso **localmente**, sem enviar dados.

## Fotografias

As imagens em `assets/` são fotografias reais do stand, obtidas a partir de anúncios com marca de água do Standvirtual. **Antes de publicação, substituir pelos ficheiros originais** fornecidos pelo stand, sem marca de água. As viaturas sem fotografia mostram um marcador identificado ("foto por adicionar").

## Passo seguinte

Ver `ARQUITETURA.md` para a estrutura de implementação em produção (Next.js App Router, camada de dados substituível por Supabase, validação server-side, SEO e performance).
