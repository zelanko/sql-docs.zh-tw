---
title: 管理 DQS 記錄檔 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
helpviewer_keywords:
- logging
- log files
- dqs log files
ms.assetid: 4fccfd24-aede-4882-be69-ec1e82682e16
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 4aa9dc994ddd11c6fad57473d20956d95e46ebeb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65484160"
---
# <a name="manage-dqs-log-files"></a>管理 DQS 記錄檔
  [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 記錄檔可幫助您診斷及排除 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]、 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]和 [!INCLUDE[ssDQSCleansingLong](../includes/ssdqscleansinglong-md.md)]的疑難問題。 系統會針對 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]、 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]和 [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)]產生個別記錄檔。  
  
 您可以使用 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 來設定 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 功能和模組的記錄嚴重性設定。 此外，您也可以針對 DQS 記錄檔設定一些其他 (進階) 設定，方法是手動變更 DQS_MAIN 資料庫中的 DQS 記錄組態設定及 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 電腦上的 XML 檔案。  
  
##  <a name="DQSServer"></a> 資料品質伺服器記錄檔  
 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 記錄檔 DQServerLog.DQS_MAIN.log 包含在 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]上執行之活動的記錄。 您如果安裝了 SQL Server 的預設執行個體，DQServerLog.DQS_MAIN.log 檔案將會位於 C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Log。 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 記錄檔包含以下資訊片段，每個片段都以直立線符號 (|) 分隔：  
  
-   日期和時間  
  
-   執行緒名稱  
  
-   執行緒識別碼  
  
-   記錄嚴重性 (嚴重錯誤、錯誤、警告、資訊和偵錯)  
  
    > [!NOTE]  
    >  偵錯記錄嚴重性與詳細資訊相同。  
  
-   UID (內部 DQS 基礎結構識別碼)  
  
-   命名空間  
  
-   類別和方法  
  
-   Message  
  
 除了這些項目以外，記錄檔也會顯示有關應用程式版本、電腦名稱、使用者名稱和作業系統的資訊。  
  
 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 記錄檔中的範例項目如下所示：  
  
```  
23-08-2013 01:45:29|[]|4|INFO|PUID|InfInfoModuleStarting|Microsoft.Ssdqs.Core.Startup.ServerInit|Starting DQS ServerInit: version [12.0.0.0], machine name [DQS-TEST], user name [NT Service\MSSQLSERVER], operating system [Microsoft Windows NT 6.1.7600.0]...  
```  
  
 DQServerLog.DQS_MAIN.log 檔案是輪替檔案，而且只要現有記錄檔超出 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 記錄組態設定中指定的輪替檔案大小上限時，就會建立新的記錄檔。 如需詳細資訊，請參閱＜ [Configure Advanced Settings for DQS Log Files](../../2014/data-quality-services/configure-advanced-settings-for-dqs-log-files.md)＞。  
  
##  <a name="DQSClient"></a> 資料品質用戶端記錄檔  
 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 記錄檔 DQClientLog.log 包含用戶端記錄。 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 記錄檔位於 %APPDATA%\SSDQS\Log。 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 記錄檔包含與伺服器記錄檔類似的一組資訊，但適用於用戶端。  
  
 就像 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 記錄檔一樣， [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 記錄檔也是輪替檔案，而且只要現有記錄檔超出 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 記錄組態設定中指定的輪替檔案大小上限時，就會建立新的記錄檔。 如需詳細資訊，請參閱＜ [Configure Advanced Settings for DQS Log Files](../../2014/data-quality-services/configure-advanced-settings-for-dqs-log-files.md)＞。  
  
##  <a name="DQSCleansing"></a> DQS 清理元件記錄檔  
 [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)] 記錄檔 DQSSSISLog.log 包括使用 [!INCLUDE[ssDQSCleansingLong](../includes/ssdqscleansinglong-md.md)]執行之活動的記錄。 [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)] 元件記錄檔位於 %APPDATA%\SSDQS\Log。 [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)] 記錄檔包含與伺服器記錄檔類似的一組資訊，但適用於 [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)]。  
  
##  <a name="RT"></a> 相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|描述如何使用 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]來設定 DQS 記錄檔的記錄嚴重性設定。|[設定 DQS 記錄檔的嚴重性層級](../../2014/data-quality-services/configure-severity-levels-for-dqs-log-files.md)|  
|描述如何手動設定 DQS 記錄檔的進階設定。|[設定 DQS 記錄檔的進階設定](../../2014/data-quality-services/configure-advanced-settings-for-dqs-log-files.md)|  
  
## <a name="see-also"></a>另請參閱  
 [DQS 管理](../../2014/data-quality-services/dqs-administration.md)  
  
  
