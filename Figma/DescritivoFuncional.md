# 1. Objetivo da Aplicação

Criar uma aplicação web que:

- Exiba todos os cosméticos disponíveis no Fortnite, de forma paginada.  
- Permita a filtragem avançada dos cosméticos.  
- Disponibilize um sistema de compra utilizando V-Bucks.  
- Ofereça gerenciamento de perfil, inventário e histórico do usuário.  
- Mantenha dados sincronizados com os endpoints externos `/cosmetics/new` e `/shop`.

---

# 2. Requisitos Funcionais (RF)

### **RF01 — Acesso público**  
O site deve ser acessível sem necessidade de login.

### **RF02 — Listagem de cosméticos**  
O sistema deve exibir todos os cosméticos, de forma paginada, com:  
- Nome  
- Imagem  
- Tipo  
- Raridade  
- Valor (quando aplicável)

### **RF03 — Ícones indicativos**  
Sempre que um cosmético for exibido, deve mostrar ícones para indicar:  
- Novo  
- Atualmente à venda  
- Já adquirido pelo usuário (quando logado)

### **RF04 — Busca e filtros**  
Deve ser possível filtrar cosméticos por:  
- Nome (texto livre)  
- Tipo (outfit, pickaxe, backpack etc.)  
- Raridade (rare, epic, legendary etc.)  
- Data de inclusão (intervalo de datas)  
- Apenas novos  
- Apenas à venda  
- Apenas em promoção

### **RF05 — Detalhamento do cosmético**  
Ao clicar em um cosmético, exibir sua página com detalhes completos.

### **RF06 — Sincronização de dados**  
A aplicação deve manter atualizados os dados provenientes dos endpoints:  
- `/cosmetics/new`  
- `/shop`

### **RF07 — Cadastro do usuário**  
O usuário pode se cadastrar usando e-mail e senha.

### **RF08 — Créditos iniciais**  
Após o cadastro, o usuário recebe **10.000 V-Bucks**.

### **RF09 — Login**  
Usuários cadastrados devem poder fazer login para acessar funcionalidades restritas.

### **RF10 — Compra de cosméticos**  
Usuários logados podem:  
- Comprar cosméticos com V-Bucks.  
- Comprar bundles (todos os itens do bundle devem ser marcados como adquiridos).

### **RF11 — Item único por usuário**  
Cada cosmético só pode ser comprado uma vez pelo mesmo usuário.

### **RF12 — Inventário de cosméticos adquiridos**  
Usuários logados podem visualizar todos os cosméticos que possuem.

### **RF13 — Devolução de cosméticos**  
O usuário pode devolver um cosmético a qualquer momento e receber o valor pago de volta.

### **RF14 — Histórico de operações**  
Exibir um histórico contendo:  
- Compras  
- Devoluções  
Com data, valor e item envolvido.

### **RF15 — Página pública de usuários**  
Exibir página paginada com:  
- Lista de usuários cadastrados  
- Perfil público ao clicar no usuário

### **RF16 — Perfil público**  
No perfil de cada usuário deve ser possível ver:  
- Nome ou identificação pública  
- Cosméticos adquiridos

---

# 3. Regras de Negócio (RN)

### **RN01 — V-Bucks iniciais**  
Todo novo usuário recebe **10.000 V-Bucks** automaticamente ao se cadastrar.

### **RN02 — Compra única**  
O mesmo usuário não pode comprar um cosmético mais de uma vez.

### **RN03 — Compra de bundle**  
Ao comprar um bundle:  
- Todos os itens que o compõem devem ser marcados como “adquiridos”.  
- O usuário não poderá recomprar nenhum item do bundle.

### **RN04 — Débito de créditos**  
O usuário só pode concluir uma compra se tiver saldo suficiente.

### **RN05 — Crédito ao devolver**  
A devolução devolve ao usuário exatamente o valor pago anteriormente.

### **RN06 — Permanência da devolução**  
Um item pode ser devolvido mesmo que:  
- Não esteja mais à venda  
- Não esteja disponível na loja atual

### **RN07 — Histórico imutável**  
Registros de compra e devolução não podem ser editados após criados.

### **RN08 — Exibição de indicadores**  
A presença de cada ícone depende exclusivamente:  
- Estado atual da API (novo, em promoção, à venda)  
- Histórico do usuário (adquirido)

### **RN09 — Sincronização periódica**  
O sistema deve atualizar os dados dos endpoints externos para manter:  
- Itens novos  
- Itens à venda  
- Itens em promoção

---

# 4. Requisitos Não Funcionais (RNF)

### **RNF01 — Desempenho**  
A listagem paginada deve carregar em poucos segundos.

### **RNF02 — Escalabilidade**  
A aplicação deve suportar aumento de acessos e dados sem perda significativa de desempenho.

### **RNF03 — Usabilidade**  
A interface deve ser responsiva e acessível em desktop e mobile.

---

# 5. Critérios de Aceitação (CA)

### **CA01 — Cadastro**  
- Dado que um usuário preenche e-mail e senha válidos  
- Quando envia o formulário  
- Então deve ser criado um usuário com 10.000 V-Bucks

### **CA02 — Login**  
- Dado que o usuário possui cadastro  
- Quando informa credenciais corretas  
- Então deve acessar sua área autenticada

### **CA03 — Compra de cosmético**  
- Dado que o usuário está logado  
- E possui saldo suficiente  
- Quando confirmar a compra  
- Então o item deve aparecer como “adquirido” em seu inventário  
- E seu saldo deve ser atualizado  
- E deve surgir um registro no histórico

### **CA04 — Compra de bundle**  
- Dado que o usuário compra um bundle  
- Então todos os itens dele devem ser marcados como adquiridos  
- E nenhum desses itens deve poder ser comprado novamente

### **CA05 — Devolução**  
- Dado que o usuário possui um cosmético  
- Quando solicita devolução  
- Então deve receber o valor de volta  
- E o item deve deixar de estar no inventário  
- E deve ser criado um registro no histórico

### **CA06 — Listagem paginada**  
- Ao acessar a página inicial  
- Deve exibir cosméticos em páginas  
- Com carregamento rápido  
- E com filtros funcionais

### **CA07 — Indicadores**  
- Cosméticos novos devem exibir o ícone "Novo"  
- Cosméticos ativos na loja devem exibir “À venda”  
- Cosméticos adquiridos devem exibir “Adquirido”

### **CA08 — Perfil público**  
- Ao acessar a página pública de usuários  
- Deve listar os usuários paginados  
- Ao clicar em um usuário  
- Deve exibir seus cosméticos adquiridos

#6. Design 

O projeto AartFortnite foi concebido e detalhado utilizando o Figma como principal ferramenta de design e prototipagem.

