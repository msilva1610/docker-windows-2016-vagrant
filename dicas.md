# Arquivos de dicas do Maurilio

## Erro encontrados: Could not load file or assembly

> Parser Error Message: Could not load file or assembly 'System.Web.Helpers, Version=1.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' or one of its dependencies. The located assembly's manifest definition does not match the assembly reference. (Exception from HRESULT: 0x80131040)

### Solução

Executar o script powershell para encontrar as versões de cada URL no diretório BIN.

```
get-childitem * -include *.dll,*.exe | foreach-object { "{0}`t{1}" -f $_.Name, [System.Diagnostics.FileVersionInfo]::GetVersionInfo($_).FileVersion }
```

### Resultado

Lista de DLLs no BIN do iCarecustomerInterActionUI

```
DIRECTV.Utilities.BankValidation.dll    1.0.0.1
log4net.dll     1.2.11.0
Microsoft.ApplicationServer.Caching.Client.dll  1.0.2912.0
Microsoft.ApplicationServer.Caching.Core.dll    1.0.2912.0
Microsoft.Practices.TransientFaultHandling.Core.dll     5.1.1209.1
Microsoft.Web.Infrastructure.dll        1.0.20105.407
Microsoft.Web.Services3.dll     3.0.5305.0
Microsoft.WindowsFabric.Common.dll      1.0.4619.0
Microsoft.WindowsFabric.Data.Common.dll 1.0.4619.0
Newtonsoft.Json.dll     9.0.1.19813
Sky.ICare.Cross.Messages.dll    1.0.0.0
Sky.ICare.CustomerInteraction.UI.dll    1.0.0.0
Sky.ICare.CustomerInteraction.ViewModels.dll    1.0.0.0
Sky.ICare.Services.Common.dll   1.0.0.0
Sky.ICare.UI.Common.Adapters.dll        1.0.0.0
Sky.ICare.UI.Common.dll 1.0.0.0
Sky.ICare.UI.Common.Models.dll  1.0.0.0
Sky.ICare.UI.Common.Process.dll 1.0.0.0
Sky.ICare.UI.Common.Proxies.dll 1.0.0.0
Sky.ICare.UI.Common.Views.dll   1.0.0.0
Sky.Infra.Cross.dll     1.5.0.*
Sky.SkyTefService.Entity.dll    0.0.0.0
System.Web.Helpers.dll  3.0.30128.0
System.Web.Mvc.dll      5.2.30128.0
System.Web.Razor.dll    3.0.30128.0
System.Web.WebPages.Deployment.dll      3.0.30128.0
System.Web.WebPages.dll 3.0.30128.0
System.Web.WebPages.Razor.dll   3.0.30128.0
```

Observar que a versão que o dot.net tentou carregar é a 1.0.0.0 e no BIN a versão existente é a 3.0.30128.0

No diretório raiz, digitar o comando dir /s system.web.helpers.dll para saber se a dll existe em outras pastas bin.

Na pasta PS ..\iCareClientes\ICareCustomerManagementUI\ICareEnterpriseWorkFlowUI\bin foi encontrado a versão 1.0.20105.407.

> System.Web.WebPages.dll 1.0.20105.407

Copiar essa verão para o BIN da pasta interaction.



