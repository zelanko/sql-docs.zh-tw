---
title: MSSQLSERVER_208 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 208 (Database Engine error)
ms.assetid: 4b1895f5-3197-4da1-af86-954c93507956
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a1b39638bf7ac09cac4a37d948ba13753ffb6d04
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "68056799"
---
# <a name="mssqlserver_208"></a>MSSQLSERVER_208
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|208|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SQ_BADOBJECT|  
|訊息文字|無效的物件名稱 '%.*ls'。|  
  
## <a name="explanation"></a>說明  
找不到指定的物件。  
  
### <a name="possible-causes"></a>可能的原因  
這項錯誤可能是由於下列其中一個問題所造成：  
  
-   未正確地指定物件。  
  
-   物件不存在目前的資料庫或指定的資料庫中。  
  
-   雖然物件存在，但是無法向使用者公開此物件。 例如，使用者可能沒有此物件的權限，或者此物件是在 EXECUTE 陳述式內部建立，但是卻在 EXECUTE 陳述式範圍的外部存取此物件。  
  
## <a name="user-action"></a>使用者動作  
請確認下列資訊並依適當情況更正陳述式。  
  
-   物件名稱的拼字是否正確。  
  
-   目前的資料庫內容是否正確。 如果您沒有指定物件的資料庫名稱，此物件就必須存在目前的資料庫中。 如需設定資料庫內容的詳細資訊，請參閱 [USE &#40;Transact-SQL&#41;](~/t-sql/language-elements/use-transact-sql.md)。  
  
-   物件是否存在系統資料表中。 若要確認資料表或其他結構描述範圍物件是否存在，請查詢 **sys.objects** 目錄檢視。 如果物件不在系統資料表中，表示物件已經刪除，或是使用者沒有檢視物件中繼資料的權限。 如需物件中繼資料的檢視權限詳細資訊，請參閱[中繼資料可見性組態](~/relational-databases/security/metadata-visibility-configuration.md)。  
  
-   物件是否包含在使用者的預設結構描述中。 如果沒有，您就必須使用 *schema_name.object_name* 的兩部分格式來指定此物件。 請注意，叫用純量值函式至少必須使用兩部分名稱。  
  
-   資料庫定序是否區分大小寫。  
  
    當資料庫使用區分大小寫的定序時，物件名稱就必須與資料庫中物件的大小寫相符。 例如，如果資料庫中含有區分大小寫的定序，當物件指定為 **MyTable** 時，以 **mytable** 或 **Mytable** 的形式查詢此物件會導致系統傳回錯誤 208，因為物件名稱不符。  
  
    您可以執行下列陳述式來確認資料庫定序。  
  
    ```  
    SELECT collation_name FROM sys.databases WHERE name = 'database_name';  
    ```  
  
    定序名稱中的縮寫 CS 表示定序會區分大小寫。 例如，Latin1_General_CS_AS 是區分大小寫而且區分腔調字的定序。 CI 則表示不區分大小寫的定序。  
  
-   使用者是否擁有存取物件的權限。 若要確認使用者對物件擁有的權限，請使用 **Has_Perms_By_Name** 系統函數。  
  
## <a name="see-also"></a>另請參閱  
[USE &#40;Transact-SQL&#41;](~/t-sql/language-elements/use-transact-sql.md)  
[中繼資料可見性組態](~/relational-databases/security/metadata-visibility-configuration.md)  
[HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](~/t-sql/functions/has-perms-by-name-transact-sql.md)  
  
