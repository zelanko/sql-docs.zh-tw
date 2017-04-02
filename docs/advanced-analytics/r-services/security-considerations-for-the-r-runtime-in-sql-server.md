---
title: "在 SQL Server 中 R 執行階段的安全性考量 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "04/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d5065197-69e6-4fce-9654-00acaecc148b
caps.latest.revision: 15
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 15
---
# 在 SQL Server 中 R 執行階段的安全性考量
  本主題提供使用的安全性考量事項概觀 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 如需有關管理服務，以及如何佈建用來執行 R 指令碼的使用者帳戶的詳細資訊，請參閱 [設定及管理進階分析延伸模組](../../advanced-analytics/r-services/configure-and-manage-advanced-analytics-extensions.md)。  
  
## 使用防火牆來限制 R 的網路存取  
 在建議的安裝方式中，使用了一項 Windows 防火牆規則來封鎖從 R 執行階段處理序傳出的所有網路存取。 您應該建立防火牆規則，以防止 R 執行階段處理序下載封裝或進行其他可能是惡意的網路呼叫。  
  
 我們強烈建議您開啟 Windows 防火牆 (或您偏好的其他防火牆)，以封鎖 R 執行階段進行的網路存取。  
  
 如果您使用其他防火牆程式，您也可以設定本機使用者帳戶或使用者帳戶集區所代表群組的規則，以建立規則來封鎖 R 執行階段傳出的網路連接。   
如需詳細資訊，請參閱 [Configure and Manage Advanced Analytics Extensions](../../advanced-analytics/r-services/configure-and-manage-advanced-analytics-extensions.md)。  
  
## 支援遠端運算內容的驗證方法 
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 建立之間的連線時，現在支援 Windows 整合式驗證和 SQL 登入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和遠端資料科學用戶端。 
  
 比方說，如果膝上型電腦上進行開發 R 解決方案，而且想要在 SQL Server 電腦上執行計算，您會建立 SQL Server 資料來源中，使用 **rx** 函式和定義的連接字串會根據 Windows 認證。 當您變更 _計算內容_ 從 SQL Server 電腦膝上型電腦，如果您的 Windows 帳戶具有必要的權限，所有的 R 程式碼會執行 SQL Server 電腦上。 此外，您的認證，也將會執行的 R 程式碼的一部分執行任何 SQL 查詢。 
 
 雖然 SQL 登入 SQL Server 資料來源也使用連接字串中，使用的登入需要 SQL Server 執行個體允許混合的模式驗證。
 
 ### 隱含的驗證
  
 一般 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 啟動 R 執行階段並執行它自己的帳戶下的 R 指令碼。 不過，如果 R 指令碼進行 ODBC 呼叫， [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 會模擬傳送命令，以確保 ODBC 呼叫不會失敗的使用者認證。 這稱為 *隱含的驗證*。 
 
 > [!IMPORTANT] 
 >
 > 隱含驗證成功，Windows 使用者群組，其包含背景工作帳戶 (根據預設， **SQLRUser**) 必須擁有 master 資料庫中的帳戶，針對執行個體，且此帳戶必須指定連接的執行個體的權限。  
  
## 不支援靜態加密  
 從 R 執行階段傳送或接收資料時，不支援透明資料加密。 影響，加密靜止 **則不會** 可套用至您儲存到磁碟或任何持續性的中繼結果的任何資料，R 指令碼中使用任何資料。  
 
 ## 另請參閱
 [輸入以下的連結描述](../../advanced-analytics/r-services/configuration-sql-server-r-services.md) 
  