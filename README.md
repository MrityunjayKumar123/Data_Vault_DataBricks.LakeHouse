Data_Vault_DataBricks.LakeHouse

Why Data Vault for an EDW Migration

Data Vault is the right choice when the migration involves:


Multiple source systems feeding the same business concept - "Customer" exists in the legacy EDW, a CRM, and an acquired company's system.

Regulatory/audit requirements — full history, no data loss, complete traceability to source.

Source volatility — source systems are being replaced mid-migration and the model must absorb structural change without a rebuild.

Parallel-run reconciliation — you need to prove new-platform numbers match legacy exactly, which insert-only, non-destructive history makes straightforward


If none of these apply and the domain is small and stable, a direct Kimball build is faster
