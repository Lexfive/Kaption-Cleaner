# Kaption.ai Cleaner

> Diagnóstico e remoção segura de componentes relacionados ao Kaption.ai no Google Chrome para Windows 10 e Windows 11.

Aplicação desktop para Windows que faz diagnóstico e remoção criteriosa de componentes do **Kaption.ai** no Google Chrome, especialmente quando há interferência no WhatsApp Web.

**Versão 1.0.0** · Desenvolvido por **Ramires Mohamed**

## Recursos

- Diagnóstico do Google Chrome e dos perfis `Default` e `Profile N`.
- Leitura de `manifest.json` das extensões; confirma referências por conteúdo, não apenas pelo nome da pasta.
- Verificação de políticas do Chrome em HKCU, HKLM e WOW6432Node.
- Busca limitada a `%APPDATA%` e `%LOCALAPPDATA%`, sem varrer o disco inteiro.
- Remoção somente de itens com evidência textual explícita de `kaption.ai` ou `kaption ai`.
- Confirmação antes de remover, encerramento controlado do Chrome, logs e relatório na tela.
- Backup em JSON dos valores de registro específicos antes da alteração.
- Solicitação de elevação via UAC apenas quando uma política HKLM exigir.
- Interface WPF nativa para Windows 10/11 e publicação single-file standalone para `win-x64`.
- Seletor de idioma: Português (Brasil) e English.
- Executável single-file compactado para reduzir o tamanho de distribuição; a primeira abertura pode levar alguns segundos extras.

## Requisitos

Para usar o executável publicado: Windows 10 ou Windows 11. Não é necessário instalar .NET, Visual Studio, PowerShell, Python, Node.js ou outro runtime.

Para compilar: .NET 8 SDK em um computador Windows.

## Como usar

1. Baixe `KaptionCleaner.exe` na página de Releases.
2. Abra o programa.
3. Clique em **VERIFICAR KAPTION.AI**.
4. Se houver itens confirmados, clique em **REMOVER KAPTION.AI** e confirme.
5. Reinicie o Google Chrome.

O botão de verificar é o modo diagnóstico: ele nunca modifica arquivos ou o Registro.

## Idiomas

Use o seletor no canto inferior direito da aplicação para alternar entre:

- Português (Brasil)
- English

## Segurança

A ferramenta não apaga favoritos, senhas, histórico, cookies, sessões, configurações gerais, perfis inteiros do Chrome nem dados do WhatsApp Web. Ela não faz varredura de todo o disco e não remove extensões simplesmente pelo nome da pasta.

Uma extensão só é marcada para remoção se o seu `manifest.json` tiver referência explícita ao Kaption.ai. Arquivos/diretórios são marcados somente se o próprio nome trouxer `kaption.ai` ou `kaption ai`, evitando falsos positivos como os arquivos da própria ferramenta. Políticas são removidas somente quando o nome ou valor contém essa evidência. Itens sem confirmação não são removidos automaticamente.

Antes de apagar itens, a ferramenta pede confirmação. Para políticas, salva um backup específico em `%LOCALAPPDATA%\KaptionCleaner\Backups`.

Use **Restaurar último backup** para restaurar os valores de política presentes no backup mais recente. A restauração não recria extensões ou arquivos já excluídos.

## Build e publicação

No diretório do projeto, execute:

```powershell
dotnet restore
dotnet build -c Release
dotnet publish .\src\KaptionCleaner\KaptionCleaner.csproj -c Release -r win-x64 --self-contained true -p:PublishSingleFile=true -p:EnableCompressionInSingleFile=true -o .\outputs\win-x64
```

O arquivo final estará em `outputs\win-x64\KaptionCleaner.exe`.

O executável é self-contained, single-file e comprimido. Ele não exige que o usuário final instale o .NET.

## Release

Anexe `KaptionCleaner.exe` em uma Release do GitHub. O usuário final só precisa baixar e abrir o arquivo.

## Estrutura

```text
src/KaptionCleaner/        Aplicação WPF
  Models/                  Resultados e itens detectados
  Services/                Scanner, políticas, limpeza, logs e elevação
assets/KaptionCleaner.ico  Ícone da aplicação
```

## Créditos

```text
Kaption.ai Cleaner
Desenvolvido por Ramires Mohamed
© 2026 Ramires Mohamed
```

## Licença

MIT. Consulte [LICENSE](LICENSE).
