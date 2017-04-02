---
title: "啟用外部指令碼伺服器組態選項 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/15/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "language-reference"
f1_keywords: 
  - "external scripts enabled"
  - "external_scripts_enabled_TSQL"
helpviewer_keywords: 
  - "啟用外部指令碼選項"
ms.assetid: 9d0ce165-8719-4007-9ae8-00f85cab3a0d
caps.latest.revision: 9
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 8
---
# 啟用外部指令碼伺服器組態選項
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  使用 **external scripts enabled** 選項以啟用具有特定遠端語言擴充功能之指令碼的執行。 此屬性將預設為關閉。 如果安裝 **Advanced Analytics Services**，則安裝程式可以選擇性地將此屬性設定為 true。  
  
||  
|-|  
|**適用於**：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至[目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)。|  
  
 您必須先啟用 external script enabled 選項，才能使用 **sp_execute_external_script** 程序來執行外部指令碼。 使用 **sp_execute_external_script** 執行以所支援語言 (例如 R) 所撰寫的指令碼。在 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 中，[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 包含與 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 一起安裝的伺服器元件，以及可將資料科學家連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的高效能環境的一組工作站工具和連線程式庫。  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式期間安裝 [進階分析擴充功能] 功能，以啟用 R 指令碼的執行。 如需詳細資訊，請參閱 [Installing Previous Versions of SQL Server R Services](../Topic/Installing%20Previous%20Versions%20of%20SQL%20Server%20R%20Services.md)。  
  
 執行下列指令碼來啟用外部指令碼。  
  
```  
sp_configure 'external scripts enabled', 1;  
RECONFIGURE;  
```  
  
 您必須重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，讓這項變更生效。  
  
## 另請參閱  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)   
 [SQL Server R 服務](../../advanced-analytics/r-services/sql-server-r-services.md)  
  
  