---
title: "設定工作階段語言 | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "錯誤 [SQL Server], 國際化考量"
  - "全球化 [SQL Server], 工作階段"
  - "時間 [SQL Server]"
  - "工作階段 [SQL Server], 語言"
  - "國際化考量 [SQL Server], 工作階段"
  - "日期 [SQL Server], 工作階段語言"
  - "全球化考量 [SQL Server], 工作階段"
  - "用戶端工作階段語言"
  - "時間 [SQL Server], 工作階段語言"
  - "訊息 [SQL Server], 國際化考量"
  - "伺服器端工作階段語言"
ms.assetid: de7f2c90-8f4f-4cfc-94cc-4933a7fd2bde
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# 設定工作階段語言
  工作階段語言可根據語言和文化喜好設定，用來設定在伺服器顯示下列元素的方式：  
  
-   錯誤訊息與其他系統訊息所使用的語言。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援所有系統錯誤字串及訊息的多個複本，而支援語言即為所提供之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 語言版本的所有語言。 您可以利用 [sys.messages](../Topic/sys.messages%20\(Transact-SQL\).md) 目錄檢視來檢視這些訊息。 在您安裝當地語系化版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，會將這些系統訊息翻譯成您所安裝的語言版本。 依預設，您也會取得美國英文版的這些訊息。 此外，您也可以使用 [sp_addmessage](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)，新增以特定語言顯示的使用者自訂訊息。  
  
-   日期和時間資料的格式。  
  
-   星期日期和月份的名稱，其中包括縮寫。  
  
-   星期的第一天。  
  
-   貨幣資料。  
  
 工作階段設定可以使用 33 種語言。 如需語言的清單，請參閱＜[sys.syslanguages](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)＞。  
  
## 從伺服器設定工作階段語言  
 若要從伺服器端設定工作階段語言，請使用 [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md)。  
  
## 從用戶端設定工作階段語言  
 您可以利用 OLE DB、ODBC 或 ADO.NET，在用戶端設定工作階段語言。 如果是 OLE DB，請使用 SSPROP_INIT_CURRENTLANGUAGE 屬性。 如需詳細資訊，請參閱[初始化和授權屬性](../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)。  
  
 如果是 ODBC，請使用 Language 關鍵字。 如需詳細資訊，請參閱 [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)。  
  
 如果是 ADO.NET，請使用 **ConnectionString** 物件的 **Current Language** 參數。 如需詳細資訊，請參閱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Data Access Components (MDAC) 軟體開發套件 (SDK) 文件集。  
  
  