# sql-hack1
SQL Injection – Write-up
Průzkum

Zadáním znaku ' došlo k chybě:

SQL Chyba: unrecognized token: "'"

To potvrzuje zranitelnost vůči SQL Injection.
Použitím ' OR 1=1 -- došlo k vypsání více záznamů.

Zjištění struktury

Pomocí ORDER BY bylo zjištěno, že dotaz má 2 sloupce.
Pomocí UNION SELECT 1,2 -- bylo ověřeno jejich zobrazení.

Tabulky byly vypsány přes sqlite_master, nalezeny users a config.
Struktura config: (key TEXT, value TEXT).

Exfiltrace dat

Payload:

' UNION SELECT key, value FROM config --

Výsledkem bylo získání vlajky ve formátu FLAG{...}.

Závěr

Zranitelnost vzniká kvůli nevalidovanému vstupu. Doporučeno použití parametrizovaných dotazů.
