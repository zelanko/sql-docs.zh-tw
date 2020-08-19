---
description: 安裝及設定語意搜尋
title: 安裝及設定語意搜尋 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], installing
- semantic search [SQL Server], configuring
ms.assetid: 2cdd0568-7799-474b-82fb-65d79df3057c
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 089d8f5a3c39cd29e04a342e19c29bfbafc7b712
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88404074"
---
# <a name="install-and-configure-semantic-search"></a>安裝及設定語意搜尋
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  描述統計語意搜尋的必要元件以及如何安裝或檢查這些必要元件。  
  
## <a name="install-semantic-search"></a>安裝語意搜尋  
  
###  <a name="check-whether-semantic-search-is-installed"></a><a name="HowToCheckInstalled"></a> 檢查是否已安裝語意搜尋  
 查詢 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md) 中繼資料函數的 **IsFullTextInstalled** 屬性。  
  
 傳回值 1 表示已安裝全文檢索搜尋和語意搜尋；傳回值 0 表示未安裝這兩個搜尋。  
  
```sql  
SELECT SERVERPROPERTY('IsFullTextInstalled');  
GO  
```  
  
###  <a name="install-semantic-search"></a><a name="BasicsSemanticSearch"></a> 安裝語意搜尋  
 若要安裝語意搜尋，請在安裝 SQL Server 期間選取 [要安裝的功能]**** 頁面上的 [搜尋的全文檢索和語意擷取]****。  
  
 統計語意搜尋相依於全文檢索搜尋。 這兩個選擇性功能會同時安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="install-the-semantic-language-statistics-database"></a>安裝語意語言統計資料庫  
 語意搜尋的其他外部相依性稱為語意語言統計資料庫。 此資料庫包含語意搜尋所需的語意語言模型。 單一語意語言統計資料庫會包含支援語意索引之所有語言的語言模型。  
  
###  <a name="check-whether-the-semantic-language-statistics-database-is-installed"></a><a name="HowToCheckDatabase"></a> 檢查是否已安裝語意語言統計資料庫  
 查詢目錄檢視 [sys.fulltext_semantic_language_statistics_database &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md)。  
  
 如果已安裝並註冊該執行個體的語意語言統計資料庫，則查詢結果會包含有關資料庫的一列資訊。  
  
```sql  
SELECT * FROM sys.fulltext_semantic_language_statistics_database;  
GO  
```  
  
###  <a name="install-attach-and-register-the-semantic-language-statistics-database"></a><a name="HowToInstallModel"></a> 安裝、附加及註冊語意語言統計資料庫  
 語意語言統計資料庫不是由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式所安裝。 若要將語意語言統計資料庫設定為語意索引的必要元件，請執行下列事項：  
  
 **1.安裝語意語言統計資料庫。**  
 
 1.  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝媒體上尋找語意語言統計資料庫，或從網站下載。  
  
        1.  在 **安裝媒體上，找到名稱為** SemanticLanguageDatabase.msi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 Windows Installer 套件。  
  
        2.  從 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 下載中心的 [Microsoft® SQL Server® 2016 Semantic Language Statistics](https://www.microsoft.com/download/details.aspx?id=52681) (Microsoft® SQL Server® 2016 語意語言統計資料) 頁面下載 Installer 套件。  
  
2.  執行 **SemanticLanguageDatabase.msi** Windows Installer 套件，以擷取資料庫和記錄檔。  
  
     您可以選擇性地變更目的地目錄。 安裝程式預設會將檔案擷取至 Program Files 資料夾中名為 **Microsoft 語意語言資料庫** 的資料夾中。 MSI 檔案包含壓縮的資料庫檔案和記錄檔。  
  
3.  將擷取的資料庫檔案和記錄檔移至檔案系統中的適當位置。  
  
     如果將檔案保留在預設位置，則不可能為另一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體擷取資料庫的另一個副本。  
  
    > [!IMPORTANT]  
    >  擷取語意語言統計資料庫時，會將有限權限指派給檔案系統中預設位置的資料庫檔案和記錄檔。 因此，如果您將資料庫保留在預設位置，則可能沒有附加資料庫的權限。 如果在嘗試附加資料庫時發生錯誤，請適當地移動檔案、檢查及修正檔案系統權限。  
  
 **2.附加語意語言統計資料庫。**
   
 使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 或使用 **FOR ATTACH** 語法呼叫 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)，將資料庫附加至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 如需詳細資訊，請參閱[資料庫卸離和附加 &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)。  
  
 資料庫名稱預設是 **semanticsdb**。 您可以選擇性地在附加資料庫時提供該資料庫不同的名稱。 您在後續步驟註冊資料庫時，必須提供此名稱。  
  
```sql  
CREATE DATABASE semanticsdb  
            ON ( FILENAME = 'C:\Microsoft Semantic Language Database\semanticsdb.mdf' )  
            LOG ON ( FILENAME = 'C:\Microsoft Semantic Language Database\semanticsdb_log.ldf' )  
            FOR ATTACH;  
GO  
```  
  
 此程式碼範例假設您已將資料庫從其預設位置移到新位置。  
  
 **3.註冊語意語言統計資料庫。** 
  
 呼叫 [sp_fulltext_semantic_register_language_statistics_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-semantic-register-language-statistics-db-transact-sql.md) 預存程序，並在附加資料庫時提供您為資料庫命名的名稱。  
  
```sql  
EXEC sp_fulltext_semantic_register_language_statistics_db @dbname = N'semanticsdb';  
GO  
```  

##  <a name="requirements-and-restrictions-for-the-semantic-language-statistics-database"></a><a name="reqinstall"></a> 語意語言統計資料庫的要求和限制  
  
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體上，您只能附加並註冊一個語意語言統計資料庫。  
  
     單一電腦上的每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體都需要語意語言統計資料庫不同的實體複本。 將一個複本附加至每個執行個體。  
  
-   您無法卸離有效且已註冊的語意語言統計資料庫，然後將它取代成具有相同名稱的任意資料庫。 這樣做會導致使用中或未來的索引母體擴展失敗。  
  
-   語意語言統計資料庫是唯讀的。 您不能自訂這個資料庫。 如果您以任何方式改變資料庫的內容，則未來語意索引的結果就不具決定性。 若要還原這項資料的原始狀態，您可以卸除已改變的資料庫，然後下載並附加全新且尚未改變的資料庫複本。  
  
-   您可以卸離或卸除語意語言統計資料庫。 如果任何使用中索引作業具有資料庫的讀取鎖定，則卸離或卸除作業將會失敗或逾時。這與現有的行為一致。 移除資料庫之後，語意索引作業將會失敗。  
 
##  <a name="remove-the-semantic-language-statistics-database"></a><a name="HowToUnregister"></a> 移除語意語言統計資料庫  

###  <a name="unregister-detach-and-remove-the-semantic-language-statistics-database"></a>取消註冊、卸離及移除語意語言統計資料庫 

 **1.取消註冊語意語言統計資料庫。**
   
 呼叫 [sp_fulltext_semantic_unregister_language_statistics_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-semantic-unregister-language-statistics-db-transact-sql.md) 預存程序。 執行個體只能有一個語意語言統計資料庫，因此您不需要提供資料庫的名稱。  
  
```sql  
EXEC sp_fulltext_semantic_unregister_language_statistics_db;  
GO  
```  
  
 **2.卸離語意語言統計資料庫。**  
 
 呼叫 [sp_detach_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md) 預存程序，並提供資料庫的名稱。  
  
```sql  
USE master;  
GO  
  
EXEC sp_detach_db @dbname = N'semanticsdb';  
GO  
```  
  
 **3.移除語意語言統計資料庫。**  
 
 取消註冊及卸離資料庫之後，就只能刪除資料庫檔案。 目前沒有解除安裝程式，而且 [控制台] 的 **[程式和功能]** 也沒有對應的項目。  
  
## <a name="install-optional-support-for-newer-document-types"></a>安裝選擇性的新版文件類型支援  
  
###  <a name="install-the-latest-filters-for-microsoft-office-and-other-microsoft-document-types"></a><a name="office"></a> 安裝 Microsoft Office 和其他 Microsoft 文件類型的最新篩選  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會安裝最新的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 斷詞工具和字幹，但是不會安裝 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office 文件和其他 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 文件類型的最新篩選。 這些篩選是針對以最新版 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office 和其他 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 應用程式建立的文件編製索引時所必要。 若要下載最新的篩選，請參閱 [Microsoft Office 2010 篩選套件](https://www.microsoft.com/download/details.aspx?id=17062)。 (這裡不會是 Office 2013 或 Office 2016 的 Filter Pack 版本)。
  
  
