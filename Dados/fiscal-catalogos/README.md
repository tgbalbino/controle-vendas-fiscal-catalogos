# Catálogos fiscais publicados

O manifesto fixo usado pelo ERP fica em `manifest.json` no repositório público `tgbalbino/controle-vendas-fiscal-catalogos`,
branch `main`; o repositório privado do ERP não precisa ser público. Cada pacote é versionado e sua URL aponta para um arquivo imutável
no mesmo diretório. O cliente valida o SHA-256 informado antes de importar e
registra a versão e o hash no banco.

Para publicar uma atualização: gerar o pacote normalizado, atualizar versão e
URL no manifesto, recalcular o SHA-256 dos bytes exatos do pacote, validar JSON,
hash e contagem com `Tests/Fiscal-Catalogos/ValidarPacotes.ps1`, e então enviar
os arquivos juntos para `main`. O aplicativo consulta o manifesto sempre que o
usuário aciona **Atualizar catálogos**; se a rede falhar, usa a cópia instalada.
O arquivo `.gitattributes` do repositório público preserva os bytes dos JSONs
para que o SHA-256 do manifesto corresponda exatamente ao conteúdo servido.

O pacote `NCM-2026.11.23.1.json` contém os 10.516 códigos NCM ativos de oito
dígitos retornados pela API pública Classif/Siscomex em 23/11/2026. O pacote
`CFOP-2026.09.04.1.json` contém 619 códigos ativos da tabela do Portal Nacional
da NF-e publicada em 04/09/2026. A origem oficial e a data estão indicadas no
pacote e no manifesto; compare a publicação original antes de renovar a tabela.

`CCLASS_TRIB-2026.10.30.1.json` foi gerado da planilha oficial SVRS v1.71,
publicada em 30/10/2026. Traz os 104 códigos com aplicação marcada para NF-e
ou NFC-e e conserva a descrição e as datas de vigência da tabela de origem.
O produto exibe código e descrição no combo, mas grava apenas o código.

Os pacotes `CST-2026.11.24.1.json` e `CSOSN-2026.11.24.1.json` usam a Tabela B
do MOC 7.00 da NF-e/NFC-e: 11 códigos CST ICMS e 10 CSOSN. O catálogo de CST
representa o domínio do campo CST ICMS, não códigos de IPI, PIS ou COFINS.

`UNIDADE_TRIBUTAVEL` é uma lista inicial de códigos usuais, mantida pelo ERP e
editável pelo cliente; não é uma tabela oficial completa da SEFAZ. A unidade é
um código informado em `uTrib`. O fator é a conversão numérica entre unidade
comercial e tributável, não um código cadastral.

Todos os catálogos são para homologação e apoio ao preenchimento. Perfil,
vigência, UF, CRT e operação ainda precisam ser validados antes de qualquer
emissão fiscal.
