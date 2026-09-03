# AutoVitrine — XR21MOTORS (conceito demonstrativo KRONUS)

Protótipo navegável de alta fidelidade. Abaixo, o mapeamento 1:1 para a implementação final em Next.js + TypeScript + Tailwind + Framer Motion + Lucide.

## Estrutura alvo (Next.js App Router)

```
app/
  layout.tsx                  metadata base, fontes, CookieConsent, WhatsAppFloat
  page.tsx                    Home (Hero → Search → Featured → Trust → Catálogo → Finance → TradeIn → Process → About → Reviews → CTA → Contact)
  viaturas/page.tsx           catálogo com filtros client-side + ordenação + contador
  viaturas/[slug]/page.tsx    página individual (generateStaticParams + generateMetadata)
  financiamento/page.tsx
  retomas/page.tsx
  contactos/page.tsx
  privacidade/page.tsx
  cookies/page.tsx
  termos/page.tsx
components/
  Header  Footer  WhatsAppFloat  CookieConsent
  VehicleCard  VehicleGrid  VehicleFilters  VehicleSearch
  VehicleGallery  VehicleSpecs  VehicleEquipment  ConversionCard  MobilePriceBar
  FinanceForm  TradeInForm  FormField  FormSuccess  Skeleton  EmptyState
sections/
  Hero  TrustStrip  FeaturedVehicles  ServicesSection  ProcessSection
  AboutSection  TestimonialSection  CTASection  ContactSection
data/
  mockVehicles.ts             dataset demonstrativo (isDemo: true)
  reviews.ts                  depoimentos (demoReview: true)
  equipment.ts                grupos de equipamento
types/
  vehicle.ts  lead.ts  finance.ts  tradeIn.ts
utils/
  format.ts                   money(), km(), power() — locale pt-PT
  whatsapp.ts                 buildWhatsAppLink(vehicle?)
  validation.ts               schemas (zod) partilhados client/server
config/
  businessConfig.ts           name, phone, whatsapp, email, address, instagram
  flags.ts                    DEMO_MODE
lib/
  vehicles.ts                 camada de dados: getVehicles/getVehicleBySlug
```

## Camada de dados

`lib/vehicles.ts` é a única fronteira: hoje devolve `mockVehicles`, amanhã Supabase.

```ts
export async function getVehicles(): Promise<Vehicle[]>
export async function getVehicleBySlug(slug: string): Promise<Vehicle | null>
```

Tabelas previstas (não configuradas): `vehicles`, `vehicle_images`, `brands`, `leads`, `finance_requests`, `trade_in_requests`.

## DEMO_MODE

`DEMO_MODE = true`: formulários validam e mostram sucesso **localmente**, sem qualquer envio de dados — evita receber dados pessoais reais durante apresentações. Rodapé mostra a assinatura discreta "Conceito demonstrativo — KRONUS Soluções Digitais".

## Segurança

- Sem chaves, tokens ou credenciais no front-end; sem login ou pagamento simulados.
- Formulários: validação client-side + limites de caracteres + sanitização básica; a mesma validação (zod) deve correr em Route Handler antes de qualquer persistência.
- Sem `dangerouslySetInnerHTML`. Links externos com `rel="noopener noreferrer"`.
- Financiamento é sempre **pedido de contacto** — nunca aprovação automática.

## RGPD

Consentimento explícito por categoria (necessários / analítica / marketing) guardado em `av_cookie_consent`; scripts opcionais só carregam após consentimento. Políticas de Privacidade, Cookies e Termos incluídas (texto a validar juridicamente).

## Performance

`next/image` com `sizes` corretos, LCP no hero com `priority`, resto em lazy loading; Framer Motion apenas em fade/slide curto e stagger discreto; zero dependências decorativas.

## Notas de conteúdo

Dados de viaturas (`isDemo: true`) e depoimentos (`demoReview: true`) são demonstrativos e não representam o stock nem reviews reais da XR21MOTORS. Não é afirmada qualquer parceria oficial entre KRONUS e XR21MOTORS.
