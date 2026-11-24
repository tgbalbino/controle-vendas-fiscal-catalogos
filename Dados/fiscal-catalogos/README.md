# Catálogos fiscais publicados

O manifesto fixo usado pelo ERP fica em `manifest.json` no repositório público de catálogos `tgbalbino/controle-vendas-fiscal-catalogos`,
branch `main`. O repositório contém somente estes pacotes e sua documentação. Cada pacote é versionado e sua URL aponta para um arquivo imutável
no mesmo diretório. O cliente valida o SHA-256 informado antes de importar e
registra a versão e o hash no banco.

Para publicar uma atualização: gerar o pacote normalizado, atualizar versão e
URL no manifesto, recalcular o SHA-256 dos bytes exatos do pacote, validar JSON,
hash e contagem com `Tests/Fiscal-Catalogos/ValidarPacotes.ps1`, e então enviar
os arquivos juntos para `main`. O aplicativo consulta o manifesto sempre que o
usuário aciona **Atualizar catálogos**; se a rede falhar, usa a cópia instalada.

O pacote `NCM-2026.11.23.1.json` contém os 10.516 códigos NCM ativos de oito
dígitos retornados pela API pública Classif/Siscomex em 23/11/2026. O pacote
`CFOP-2026.09.04.1.json` contém 619 códigos ativos da tabela do Portal Nacional
da NF-e publicada em 04/09/2026. A origem oficial e a data estão indicadas no
pacote e no manifesto; compare a publicação original antes de renovar a tabela.

`UNIDADE_TRIBUTAVEL` é uma lista inicial de códigos usuais, mantida pelo ERP e
editável pelo cliente; não é uma tabela oficial completa da SEFAZ. A unidade é
um código informado em `uTrib`. O fator é a conversão numérica entre unidade
comercial e tributável, não um código cadastral.

Todos os catálogos são para homologação e apoio ao preenchimento. Perfil,
vigência, UF, CRT e operação ainda precisam ser validados antes de qualquer
emissão fiscal.
