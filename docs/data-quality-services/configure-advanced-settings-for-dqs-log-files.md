---
title: "設定 DQS 記錄檔的進階設定 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: 
ms.component: data-quality-services
ms.reviewer: 
ms.suite: sql
ms.technology: data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- log files,advanced settings
- dqs log files,advanced settings
ms.assetid: 1d565748-9759-425c-ae38-4d2032a86868
caps.latest.revision: "13"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 806fd99943d21f48e5e9b2b4600482f2f0079de1
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="configure-advanced-settings-for-dqs-log-files"></a>為 DQS 記錄檔設定進階設定
  本主題描述如何設定 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 和 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 記錄檔的進階設定，例如設定記錄檔的輪替檔案大小限制、設定事件的時間戳記模式等等。  
  
> [!NOTE]  
>  這些活動無法使用 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]來執行，而且僅適用於進階使用者。  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
  
-   您的 Windows 使用者帳戶必須是 SQL Server 執行個體上系統管理員 (sysadmin) 固定伺服器角色的成員，才能修改 DQS_MAIN 資料庫中 A_CONFIGURATION 資料表的組態設定。  
  
-   您必須在想要修改 DQLog.Client.xml 檔案的電腦上，以 Administrators 群組成員的身分登入，才能設定 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 記錄設定。  
  
##  <a name="DQSServer"></a> 設定 Data Quality Server 記錄設定  
 在 DQS_MAIN 資料庫的 A_CONFIGURATION 資料表中， [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 記錄設定會以 XML 格式存在 **[ServerLogging]** 資料列的 **[VALUE]** 資料行中。 您可以執行下列 SQL 查詢，以便檢視組態資訊：  
  
```  
select * from DQS_MAIN.dbo.A_CONFIGURATION where NAME='ServerLogging'  
```  
  
 若要變更  記錄的組態設定，您必須在 **[ServerLogging]** 資料列的 [VALUE] [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 資料行中更新適當資訊。 在此範例中，我們將更新 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 記錄設定，以便將輪替檔案大小限制設定為 25000 KB (預設值為 20000 KB)。  
  
1.  啟動 Microsoft SQL Server Management Studio，並連接到適當的 SQL Server 執行個體。  
  
2.  在 [物件總管] 中，以滑鼠右鍵按一下伺服器，然後按一下 **[新增查詢]**。  
  
3.  在 [查詢編輯器] 視窗中，複製下列 SQL 陳述式：  
  
    ```  
    -- Begin the transaction.  
    BEGIN TRAN  
    GO  
    -- set the XML value field for the row with name=ServerLogging  
    update DQS_MAIN.dbo.A_CONFIGURATION   
    set VALUE='<configuration>  
      <configSections>  
        <section name="loggingConfiguration" type="Microsoft.Practices.EnterpriseLibrary.Logging.Configuration.LoggingSettings, Microsoft.Practices.EnterpriseLibrary.Logging, Version=4.1.0.0, Culture=neutral, PublicKeyToken=e44a2bc38ed2c13c" />  
      </configSections>  
      <loggingConfiguration name="Logging Application Block" tracingEnabled="true" defaultCategory="" logWarningsWhenNoCategoriesMatch="true">  
        <listeners>  
          <add fileName="###REPLACE_THIS_WITH_SQL_SERVER_INSTANCE_LOG_FOLDER_NAME###DQServerLog.###REPLACE_THIS_WITH_SQL_CATALOG_NAME###.log" footer="" formatter="Custom Text Formatter" header="" rollFileExistsBehavior="Increment" rollInterval="None" rollSizeKB="25000" timeStampPattern="yyyy-MM-dd" listenerDataType="Microsoft.Practices.EnterpriseLibrary.Logging.Configuration.RollingFlatFileTraceListenerData, Microsoft.Practices.EnterpriseLibrary.Logging, Version=4.1.0.0, Culture=neutral, PublicKeyToken=e44a2bc38ed2c13c" traceOutputOptions="None" filter="All" type="Microsoft.Practices.EnterpriseLibrary.Logging.TraceListeners.RollingFlatFileTraceListener, Microsoft.Practices.EnterpriseLibrary.Logging, Version=4.1.0.0, Culture=neutral, PublicKeyToken=e44a2bc38ed2c13c" name="Rolling Flat File Trace Listener" />  
        </listeners>  
        <formatters>  
          <add template="{timestamp(local)}|[{threadName}]|{dictionary({value}|)}{message}" type="Microsoft.Practices.EnterpriseLibrary.Logging.Formatters.TextFormatter, Microsoft.Practices.EnterpriseLibrary.Logging, Version=4.1.0.0, Culture=neutral, PublicKeyToken=e44a2bc38ed2c13c" name="Custom Text Formatter" />  
        </formatters>  
        <logFilters>  
          <add enabled="true" type="Microsoft.Practices.EnterpriseLibrary.Logging.Filters.LogEnabledFilter, Microsoft.Practices.EnterpriseLibrary.Logging, Version=4.1.0.0, Culture=neutral, PublicKeyToken=e44a2bc38ed2c13c" name="LogEnabled Filter" />  
        </logFilters>  
        <categorySources />  
        <specialSources>  
          <allEvents switchValue="All" name="All Events" />  
          <notProcessed switchValue="All" name="Unprocessed Category" />  
          <errors switchValue="All" name="Logging Errors & Warnings">  
            <listeners>  
              <add name="Rolling Flat File Trace Listener" />  
            </listeners>  
          </errors>  
        </specialSources>  
      </loggingConfiguration>  
    </configuration>'  
    WHERE NAME='ServerLogging'  
    GO  
    -- check the result  
    select * from DQS_MAIN.dbo.A_CONFIGURATION where NAME='ServerLogging'  
  
    -- Commit the transaction.  
    COMMIT TRAN  
  
    ```  
  
4.  按 F5 執行陳述式。 檢查 **[結果]** 窗格，確認陳述式是否皆已成功地執行。  
  
5.  若要將所做的變更套用至 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 記錄組態，您必須執行下列 Transact-SQL 陳述式。 開啟新的 [查詢編輯器] 視窗，並且貼上下列 Transact-SQL 陳述式：  
  
    ```  
    USE [DQS_MAIN]  
    GO  
    DECLARE @return_value int  
    EXEC @return_value = [internal_core].[RefreshLogSettings]  
    SELECT 'Return Value' = @return_value  
    GO  
  
    ```  
  
6.  按 F5 執行陳述式。 檢查 **[結果]** 窗格，確認陳述式是否皆已成功地執行。  
  
> [!NOTE]  
>  [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 記錄設定組態是以動態方式產生並儲存在 DQS_MAIN.Log 檔案中，而該檔案通常位於 C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Log (如果您安裝了 SQL Server 預設執行個體的話)。 不過，直接在此檔案中進行的變更不會保存，而且 DQS_MAIN 資料庫中 A_CONFIGURATION 資料表的組態設定會覆寫這些變更。  
  
##  <a name="DQSClient"></a> 設定 Data Quality Client 記錄設定  
 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 記錄設定組態檔 DQLog.Client.xml 通常位於 C:\Program Files\Microsoft SQL Server\130\Tools\Binn\DQ\config。此 XML 檔案的內容與您之前針對 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 記錄組態設定所修改的 XML 檔案很相似。 若要設定 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 記錄設定：  
  
1.  以系統管理員的身分執行任何 XML 編輯工具或 [記事本]。  
  
2.  在工具或 [記事本] 中開啟 DQLog.Client.xml 檔案。  
  
3.  進行所需的變更，然後儲存檔案，即可套用新的記錄變更。  
  
## <a name="see-also"></a>另請參閱  
 [設定 DQS 記錄檔的嚴重性層級](../data-quality-services/configure-severity-levels-for-dqs-log-files.md)  
  
  
