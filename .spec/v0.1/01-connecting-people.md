# ESPECIFICAÇÃO DE SOFTWARE: Plataforma de Serviços Voluntários (MVP)

## 1. Visão Geral do Produto
Plataforma web/mobile voltada para caridade e ação social que conecta profissionais voluntários (médicos, advogados, mecânicos, motoristas, etc.) a pessoas em situação de vulnerabilidade que necessitam desses serviços gratuitamente, priorizando a geolocalização/proximidade física.

## 2. Personas e Casos de Uso
1. **Voluntário (Provedor do Serviço):**
   - Cadastra perfil com profissão/especialidade.
   - Informa se atende presencialmente (com endereço/raio de atuação) ou online.
   - Define seus horários e dias disponíveis em uma agenda simples.
   - Aceita ou recusa solicitações de agendamento.
2. **Beneficiário (Solicitante do Serviço):**
   - Busca serviços por categoria e localização/proximidade.
   - Visualiza perfil do voluntário e horários vagos.
   - Solicita agendamento informando brevemente a sua necessidade.
3. **Administrador:**
   - Valida/aprova o cadastro de novos voluntários para segurança do sistema.

## 3. Funcionalidades Essenciais (Escopo do MVP)

### A. Autenticação e Perfis
- Cadastro e Login (E-mail/Senha).
- Seleção do Tipo de Conta: `Voluntário` ou `Beneficiário`.
- **Perfil do Voluntário:** Nome, Foto, Categoria Profissional (Ex: Medicina, Advocacia, Transporte, Mecânica, Outros), Descrição, Cidade/Bairro ou Geolocalização, Modalidade (Presencial, Remoto, Ambas).
- **Perfil do Beneficiário:** Nome, Cidade/Bairro, Telefone de contato (WhatsApp).

### B. Módulo de Proximidade e Busca
- Listagem e busca de serviços filtrando por:
  1. Categoria do profissional.
  2. Cidade/Bairro ou distância (ordenado pelos mais próximos).
  3. Modalidade (Presencial/Online).

### C. Agendamento e Agenda do Voluntário
- **Definição de Horários:** O voluntário marca dias da semana e blocos de horários em que pode atender gratuitamente.
- **Reserva de Horário:** O beneficiário escolhe um horário disponível na agenda do voluntário e envia o pedido.
- **Confirmação:** Notificação ou status no painel (`Pendente`, `Confirmado`, `Cancelado`, `Concluído`).
- **Comunicação Básica:** Exibição do WhatsApp/Telefone para contato direto após a confirmação do agendamento.

## 4. Arquitetura Técnica Sugerida
- **Frontend:** Next.js (React) com Tailwind CSS (design responsivo, funciona bem em celular e PC).
- **Backend/Banco de Dados:** Supabase ou Firebase (Facilita autenticação, banco de dados relacional/NoSQL e API pronta sem precisar reescrever tudo do zero).
- **Geolocalização:** API de mapas simples (Leaflet / OpenStreetMap - 100% gratuito) ou busca por Cidade/Bairro.

## 5. Modelo de Dados Simplificado (Banco de Dados)

1. `Users` (id, name, email, role ['VOLUNTEER', 'BENEFICIARY'], phone, city, state, lat, lng, bio, created_at)
2. `Categories` (id, name [Medicina, Advocacia, Mecânica, Transporte, etc.])
3. `VolunteerProfiles` (user_id, category_id, is_remote, service_radius_km)
4. `Schedules` (id, volunteer_id, day_of_week, start_time, end_time, is_booked)
5. `Appointments` (id, volunteer_id, beneficiary_id, schedule_id, status ['PENDING', 'CONFIRMED', 'CANCELLED', 'COMPLETED'], description)

## 6. Instruções de Desenvolvimento
Gere o projeto passo a passo na seguinte ordem:
1. Estrutura do banco de dados (SQL / Schema Supabase ou Prisma).
2. Páginas de cadastro/login e criação de perfil.
3. Dashboard do voluntário (onde ele cadastra seus horários disponíveis).
4. Tela de busca e filtros de serviços por proximidade/categoria.
5. Fluxo de agendamento do beneficiário.