# 🍽️ Controle de Almoço (QR Code)

Sistema simples e rápido para controle de acesso ao restaurante/almoço através de leitura de QR Code via câmera, integrado diretamente ao **Supabase** e hospedado no **GitHub Pages**.

---

## 🚀 Como Funciona

1. O operador clica em **Ligar Câmera** e aproxima o QR Code/crachá.
2. O aplicativo faz a verificação instantânea no banco de dados:
   * ❌ **BLOQUEADO:** Caso o código já tenha sido registrado no banco (já almoçou).
   * ✅ **ALMOÇO LIBERADO:** Caso seja a primeira leitura (grava o registro e libera o acesso).

---

## 🛠️ Tecnologias Utilizadas

* **Frontend:** HTML5, CSS3, JavaScript puro
* **Leitor QR Code:** [Html5-QRCode](https://github.com/mebjas/html5-qrcode)
* **Banco de Dados:** [Supabase](https://supabase.com/)
* **Hospedagem:** GitHub Pages

---

## ⚙️ Configuração do Banco (Supabase)

Para rodar este projeto, a tabela `almoco` precisa estar criada e com as políticas de **RLS (Row Level Security)** ativas para permitir consulta e inserção públicas:

```sql
-- Ativa RLS
ALTER TABLE almoco ENABLE ROW LEVEL SECURITY;

-- Permite consultar se o crachá já almoçou (SELECT)
CREATE POLICY "Permitir leitura publica" 
ON almoco FOR SELECT 
TO anon 
USING (true);

-- Permite gravar novo almoço (INSERT)
CREATE POLICY "Permitir insercao publica" 
ON almoco FOR INSERT 
TO anon 
WITH CHECK (true);
