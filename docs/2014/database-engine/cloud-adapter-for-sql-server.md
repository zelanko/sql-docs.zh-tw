---
title: SQL Server 的雲端配接器 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Cloud adapter
- Deploy to Azure
ms.assetid: 82ed0d0f-952d-4d49-aa36-3855a3ca9877
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bf57adb31330f5b0c0f18fbcccd4d71f47d3c933
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "70176013"
---
# <a name="cloud-adapter-for-sql-server"></a>適用 SQL Server 的雲端配接器
  在 Azure VM 上布建的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]過程中，會建立雲端配接器服務。 雲端配接器服務會在其初次執行時產生自我簽署 SSL 憑證，然後以 **本機系統** 帳戶執行。 它會產生用來設定本身的組態檔。 雲端配接器也會建立 Windows 防火牆規則，以允許其在預設通訊埠 11435 的傳入 TCP 連接。  
  
 雲端配接器是無狀態的同步服務，可從 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的內部部署執行個體接收訊息。 當雲端配接器服務停止時，它會停止遠端存取雲端配接器、將 SSL 憑證解除繫結，並且停用 Windows 防火牆規則。  
  
## <a name="cloud-adapter-requirements"></a>雲端配接器需求  
 請注意下列 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]適用之安裝、啟用和執行雲端配接器的需求：  
  
-   雲端配接器可在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2012 及更高版本上支援。 在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2012 上，適用於 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的雲端配接器需要 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2012 適用的 SQL 管理物件。  
  
-   雲端配接器 Web 服務會以 **本機系統** 帳戶執行，並且在執行任何工作之前驗證用戶端認證。 用戶端提供的認證必須屬於遠端電腦上本機系統**管理員**群組成員的使用帳戶。  
  
-   雲端配接器只支援 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證。  
  
-   雲端配接器使用 VM 本機系統管理員帳戶在本機電腦上執行命令，而非 sa 帳戶。  
  
-   雲端配接器會接聽 TCP/IP。 預設通訊埠是 11435。  
  
-   雲端配接器必須具有建立及修改 Windows 防火牆規則的權限。  
  
## <a name="cloud-adapter-configuration-settings"></a>雲端配接器組態設定  
 請使用下列雲端配接器組態詳細資料修改雲端配接器的設定。  
  
-   **設定檔案的預設路徑**-C:\PROGRAM Files\Microsoft SQL Server\120\Tools\CloudAdapter\  
  
-   **設定檔參數** -  
  
    -   \<configuration>  
  
        -   \<appSettings>  
  
            -   \<add key = "WebServicePort" value = ""/>  
  
            -   \<add key = "WebServiceCertificate" value = "GUID"/>  
  
            -   \<add key = "ExposeExceptionDetails" value = "true"/>  
  
        -   \</appSettings>  
  
    -   \</組態>  
  
-   **憑證詳細資料**-憑證具有下列值：  
  
    -   Subject-"CN = CloudAdapter\<VMName>，dc = SQL SERVER，DC = Microsoft"  
  
    -   憑證應只啟用伺服器驗證 EKU。  
  
    -   憑證金鑰長度為 2048。  
  
 **設定檔值**：  
  
|設定|值|預設|評價|  
|-------------|------------|-------------|--------------|  
|WebServicePort|1-65535|11435|若未指定，則使用 11435。|  
|WebServiceCertificate|指模|空白|如為空白，則會產生新的自我簽署憑證。|  
|ExposeExceptionDetails|True/False|False||  
  
## <a name="cloud-adapter-troubleshooting"></a>雲端配接器疑難排解  
 請利用下列資訊對 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]適用的雲端配接器進行疑難排解：  
  
-   **錯誤處理和記錄**-錯誤和狀態訊息會寫入應用程式事件記錄檔。  
  
-   **追蹤、事件**-所有事件都會寫入應用程式事件記錄檔。  
  
-   **控制，** 設定-使用位於下列位置的設定檔： C:\PROGRAM Files\Microsoft SQL\\Server\120\Tools\CloudAdapter。  
  
|錯誤|錯誤識別碼|原因|解決方法|  
|-----------|--------------|-----------|----------------|  
|將憑證加入至憑證存放區時發生例外狀況。 {例外狀況文字}。|45560|電腦憑證存放區權限。|請確認雲端配接器服務具有將憑證加入至電腦憑證存放區的權限。|  
|嘗試設定通訊埠 {通訊埠號碼} 和憑證 {指模} 的 SSL 繫結時發生例外狀況。 {例外狀況}。|45561|其他應用程式已使用該通訊埠並將憑證繫結至該通訊埠。|請移除現有繫結，或變更組態檔中的雲端配接器通訊埠。|  
|憑證存放區中找不到 SSL 憑證 [{指模}]。|45564|憑證指模位於組態檔中，但服務的個人憑證存放區未包含憑證。<br /><br /> 權限不足。|請確認憑證位於個人服務的個人憑證存放區中。<br /><br /> 請確認服務具有正確的存放區權限。|  
|無法啟動 Web 服務。 {例外狀況文字}。|45570|於例外狀況中描述。|請啟用 ExposeExceptionDetails 並使用例外狀況中的擴充資訊。|  
|憑證 [{指模}] 已過期。|45565|從組態檔參考的憑證已過期。|請加入有效的憑證，並以其指模更新組態檔。|  
|Web 服務錯誤： {0}。|45571|於例外狀況中描述。|請啟用 ExposeExceptionDetails 並使用例外狀況中的擴充資訊。|  
  
## <a name="see-also"></a>另請參閱  
 [將 SQL Server Database 部署到 Microsoft Azure 虛擬機器](../relational-databases/databases/deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine.md)  
  
  
