---
title: 安裝及設定語意搜尋 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], installing
- semantic search [SQL Server], configuring
ms.assetid: 2cdd0568-7799-474b-82fb-65d79df3057c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 164ae15bdd93034ebcca109a01142b3106a78592
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "73637912"
---
# <a name="install-and-configure-semantic-search"></a>安裝及設定語意搜尋
  描述統計語意搜尋的必要元件以及如何安裝或檢查這些必要元件。  
  
## <a name="installing-semantic-search"></a>安裝語意搜尋  
  
###  <a name="HowToCheckInstalled"></a>如何：檢查是否已安裝語義搜尋  
 查詢 [SERVERPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql) 中繼資料函數的 **IsFullTextInstalled** 屬性。  
  
 傳回值 1 表示已安裝全文檢索搜尋和語意搜尋；傳回值 0 表示未安裝這兩個搜尋。  
  
```sql  
SELECT SERVERPROPERTY('IsFullTextInstalled');  
GO  
```  
  
###  <a name="BasicsSemanticSearch"></a>如何：安裝語義搜尋  
 若要安裝語意搜尋，請在安裝期間選取 [要安裝的功能]**** 頁面上的 [搜尋的全文檢索和語意擷取]****。  
  
 統計語意搜尋相依於全文檢索搜尋。 這兩個選擇性功能會同時安裝 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
## <a name="installing-or-removing-the-semantic-language-statistics-database"></a>安裝或移除語意語言統計資料庫  
 語意搜尋的其他外部相依性稱為語意語言統計資料庫。 此資料庫包含語意搜尋所需的語意語言模型。 單一語意語言統計資料庫會包含支援語意索引之所有語言的語言模型。  
  
###  <a name="HowToCheckDatabase"></a>如何：檢查是否已安裝語意語言統計資料資料庫  
 查詢目錄檢視 [sys.fulltext_semantic_language_statistics_database &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql)。  
  
 如果已安裝並註冊該執行個體的語意語言統計資料庫，則查詢結果會包含有關資料庫的一列資訊。  
  
```vb  
SELECT * FROM sys.fulltext_semantic_language_statistics_database;  
GO  
```  
  
###  <a name="HowToInstallModel"></a>如何：安裝、附加及註冊語意語言統計資料資料庫  
 語意語言統計資料庫不是由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝程式所安裝。 若要將語意語言統計資料庫設定為語意索引的必要元件，請執行下列工作：  
  
 **1.安裝語意語言統計資料庫。**  
 1.  在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安裝媒體上尋找語意語言統計資料庫，或從網站下載。  
  
    -   在 **安裝媒體上，找到名稱為** SemanticLanguageDatabase.msi [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的 Windows Installer 套件。 找到 32 位元或 64 位元版本的 Installer 套件 (視目標系統而定)。 包含資料夾名稱可識別檔案的 32 位元或 64 位元版本；這兩種版本的檔案名稱本身相同。  
  
    -   要從 Microsoft 下載安裝程式套件[嗎？SQL Server？？2014語意語言統計資料](https://go.microsoft.com/fwlink/?LinkID=296743)] 頁面上[!INCLUDE[msCoName](../../../includes/msconame-md.md)]的 [下載中心]。  
  
2.  執行 **SemanticLanguageDatabase.msi** Windows Installer 套件，以擷取資料庫和記錄檔。  
  
     您可以選擇性地變更目的地目錄。 根據預設，安裝程式會將檔案解壓縮至32位或64位 Program Files 資料夾中名為**Microsoft 語義語言資料庫**的資料夾。 MSI 檔案包含壓縮的資料庫檔案和記錄檔。  
  
3.  將擷取的資料庫檔案和記錄檔移至檔案系統中的適當位置。  
  
     如果將檔案保留在預設位置，則不可能為另一個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體擷取資料庫的另一個副本。  
  
> [!IMPORTANT]  
>  擷取語意語言統計資料庫時，會將有限權限指派給檔案系統中預設位置的資料庫檔案和記錄檔。 因此，如果您將資料庫保留在預設位置，則可能沒有附加資料庫的權限。 如果在嘗試附加資料庫時發生錯誤，請適當地移動檔案、檢查及修正檔案系統權限。  
  
 **2. 附加語義語言統計資料庫。**  
 使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 或使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]FOR ATTACH[ 語法呼叫 ](/sql/t-sql/statements/create-database-sql-server-transact-sql)CREATE DATABASE &#40;SQL Server Transact-SQL&#41;**，將資料庫附加至 ** 執行個體。 如需詳細資訊，請參閱[資料庫卸離和附加 &#40;SQL Server&#41;](../databases/database-detach-and-attach-sql-server.md)。  
  
 資料庫名稱預設是 **semanticsdb**。 您可以選擇性地在附加資料庫時提供該資料庫不同的名稱。 您在後續步驟註冊資料庫時，必須提供此名稱。  
  
```sql  
CREATE DATABASE semanticsdb  
            ON ( FILENAME = 'C:\Microsoft Semantic Language Database\semanticsdb.mdf' )  
            LOG ON ( FILENAME = 'C:\Microsoft Semantic Language Database\semanticsdb_log.ldf' )  
            FOR ATTACH;  
GO  
```  
  
 此程式碼範例假設您已將資料庫從其預設位置移到新位置。  
  
 **3. 註冊語義語言統計資料庫。**  
 呼叫 [sp_fulltext_semantic_register_language_statistics_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-semantic-register-language-statistics-db-transact-sql) 預存程序，並在附加資料庫時提供您為資料庫命名的名稱。  
  
```sql  
EXEC sp_fulltext_semantic_register_language_statistics_db @dbname = N'semanticsdb';  
GO  
```  
  
###  <a name="HowToUnregister"></a>如何：取消註冊、卸離及移除語意語言統計資料資料庫  
 **取消註冊語義語言統計資料庫。**  
 呼叫 [sp_fulltext_semantic_unregister_language_statistics_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-semantic-unregister-language-statistics-db-transact-sql) 預存程序。 執行個體只能有一個語意語言統計資料庫，因此您不需要提供資料庫的名稱。  
  
```sql  
EXEC sp_fulltext_semantic_unregister_language_statistics_db;  
GO  
```  
  
 **卸離語義語言統計資料庫。**  
 呼叫 [sp_detach_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-detach-db-transact-sql) 預存程序，並提供資料庫的名稱。  
  
```sql  
USE master;  
GO  
  
EXEC sp_detach_db @dbname = N'semanticsdb';  
GO  
```  
  
 **移除語義語言統計資料庫。**  
 取消註冊及卸離資料庫之後，就只能刪除資料庫檔案。 目前沒有解除安裝程式，而且 [控制台] 的 **[程式和功能]** 也沒有對應的項目。  
  
###  <a name="reqinstall"></a>安裝和移除語意語言統計資料資料庫的需求和限制  
  
-   在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]執行個體上，您只能附加並註冊一個語意語言統計資料庫。  
  
     單一電腦上的每個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體都需要語意語言統計資料庫不同的實體複本。 將一個複本附加至每個執行個體。  
  
-   您無法卸離有效且已註冊的語意語言統計資料庫，然後將它取代成具有相同名稱的任意資料庫。 這樣做會導致使用中或未來的索引母體擴展失敗。  
  
-   語意語言統計資料庫是唯讀的。 您不能自訂這個資料庫。 如果您以任何方式改變資料庫的內容，則未來語意索引的結果就不具決定性。 若要還原這項資料的原始狀態，您可以卸除已改變的資料庫，然後下載並附加全新且尚未改變的資料庫複本。  
  
-   您可以卸離或卸除語意語言統計資料庫。 如果有任何作用中的索引作業在資料庫上有讀取鎖定，則卸離或卸載操作將會失敗或超時。這與現有的行為一致。 移除資料庫之後，語意索引作業將會失敗。  
  
## <a name="installing-optional-support-for-newer-document-types"></a>安裝選擇性的新版文件類型支援  
  
###  <a name="office"></a>如何：安裝 Microsoft Office 和其他 Microsoft 檔案類型的最新篩選  
 此版本的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會安裝最新的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 斷詞工具和字幹，但是不會安裝 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Office 文件和其他 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 文件類型的最新篩選。 這些篩選是針對以最新版 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Office 和其他 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 應用程式建立的文件編製索引時所必要。 若要下載最新的篩選，請參閱 [Microsoft Office 2010 篩選套件](https://www.microsoft.com/download/details.aspx?id=17062)。  
  
  
