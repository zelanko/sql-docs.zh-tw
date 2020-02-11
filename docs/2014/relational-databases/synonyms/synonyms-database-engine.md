---
title: 同義字 (Database Engine) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- synonyms [SQL Server], about synonyms
ms.assetid: 6210e1d5-075f-47e4-ac8d-f84bcf26fbc0
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2066eeb7d9b86228ed86aed290e69f2a0e981b95
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62736238"
---
# <a name="synonyms-database-engine"></a>同義字 (Database Engine)
  同義字是具有下列用途的資料庫物件：  
  
-   對在本機或遠端伺服器上的另一個資料庫物件 (稱為基底物件) 提供別名。  
  
-   提供抽象層來保護用戶端應用程式，避免變更基底物件的名稱或位置。  
  
 例如，以位於伺服器 **Server1** 上 [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)]的 **Employee**資料表為例。 若要從另一個伺服器 **Server2**參考此資料表，用戶端應用程式使用的名稱必須包含四個部分： **Server1.AdventureWorks.Person.Employee**。 另外，若是資料表的位置已變更 (例如，變更至另一個伺服器)，則必須修改用戶端應用程式以反映該變更。  
  
 若要解決這些問題，您可以在 **Server2**上建立同義字 **EmpTable** ，來代表 **Server1** 的 **Employee**資料表。 現在，用戶端應用程式只需要使用 **EmpTable**單一部分的名稱，即可參考 **Employee** 資料表。 此外，如果 **Employee** 資料表的位置變更，您必須修改同義字 **EmpTable**以指向 **Employee** 資料表的新位置。 由於沒有 ALTER SYNONYM 陳述式，因此您必須先卸除同義字 **EmpTable**，再以相同的名稱重新建立同義字，但要將同義字指向 **Employee**的新位置。  
  
 同義字放在結構描述中，如同結構描述中的其他物件一樣，同義字的名稱也必須是唯一的。 您可以為下列資料庫物件建立同義字：  
  
|||  
|-|-|  
|組件 (CLR) 預存程序|組件 (CLR) 資料表值函式|  
|組件 (CLR) 純量函數|組件 (CLR) 彙總函式|  
|複寫篩選程序|擴充預存程序|  
|SQL 純量函數|SQL 資料表值函式|  
|SQL 內嵌資料表值函式|SQL 預存程序|  
|檢視|資料表<sup>1</sup> (使用者定義)|  
  
 <sup>1</sup>包含本機和全域臨時表  
  
> [!NOTE]  
>  不支援函數基底物件的四部份名稱。  
  
 同義字不可為另一個同義字的基底物件，而且同義字不可以參考使用者自訂的彙總函式。  
  
 同義字和基底物件之間只透過名稱繫結。 基底物件的存在性、類型及權限，全部會延遲到執行階段再檢查。 因此，和原始基底物件名稱相同的另一個物件，可以修改、卸除或卸除並取代基底物件。 例如，以同義字 **MyContacts**為例，此同義字參考 **中的** Person.Contact [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)]資料表。 如果 **Contact** 資料表被卸除並由名稱為 **Person.Contact**的檢視所取代，則 **MyContacts** 會變成參考 **Person.Contact** 檢視。  
  
 同義字的參考不受結構描述的約束。 因此，隨時可以卸除同義字。 不過，如果卸除同義字，已卸除的同義字有可能會留下懸吊參考。 只有等到執行階段才會發現這種參考。  
  
## <a name="synonyms-and-schemas"></a>同義字和結構描述  
 如果預設的結構描述不是由您擁有，但您想要建立同義字，則必須使用您擁有的結構描述名稱來限定同義字名稱。 例如，如果您擁有結構描述 **x**，但預設結構描述是 **y** ，且您使用 CREATE SYNONYM 陳述式，則必須以結構描述 **x**作為同義字名稱的前置詞，而非使用單一部分的名稱來命名同義字。 如需如何建立同義字的詳細資訊，請參閱 [CREATE SYNONYM &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-synonym-transact-sql)資料表為例。  
  
## <a name="granting-permissions-on-a-synonym"></a>授與同義字的權限  
 只有同義字擁有者、 **db_owner**的成員或 **db_ddladmin** 的成員，才可授與同義字的權限。  
  
 您可以 GRANT、DENY、REVOKE 同義字上的任何或所有下列權限：  
  
|||  
|-|-|  
|CONTROL|刪除|  
|執行 CREATE 陳述式之前，請先執行|Insert|  
|SELECT|TAKE OWNERSHIP|  
|UPDATE|VIEW DEFINITION|  
  
## <a name="using-synonyms"></a>使用同義字  
 您可以使用同義字在數個 SQL 陳述式和運算式內容中取代其參考的基底物件。 下表包含這些陳述式及運算式內容的清單：  
  
|||  
|-|-|  
|SELECT|Insert|  
|UPDATE|刪除|  
|執行 CREATE 陳述式之前，請先執行|子 SELECT|  
  
 當您正在先前陳述的內容中使用同義字時，基底物件會受影響。 例如，如果同義字參考的基底物件是資料表，而且您將資料列插入同義字，則實際上您是將資料列插入參考的資料表。  
  
> [!NOTE]  
>  您無法參考位於連結伺的服器上的同義字。  
  
 您可以使用同義字做為 OBJECT_ID 函數的參數。不過，此函數會傳回同義字的物件識別碼，而非基底物件。  
  
 您無法在 DDL 陳述式中參考同義字。 例如，下列陳述式 (參考名為 `dbo.MyProduct`的同義字) 會產生錯誤：  
  
```  
ALTER TABLE dbo.MyProduct  
   ADD NewFlag int null;  
EXEC ('ALTER TABLE dbo.MyProduct  
   ADD NewFlag int null');  
```  
  
 下列權限陳述式只與同義字有關聯，但與基底物件無關：  
  
|||  
|-|-|  
|GRANT|拒絕|  
|REVOKE||  
  
 同義字不是結構描述繫結性質，因此，下列結構描述繫結的運算式內容無法參考同義字：  
  
|||  
|-|-|  
|CHECK 條件約束|計算資料行|  
|預設運算式|規則運算式|  
|結構描述繫結的檢視|結構描述繫結的函數|  
  
 如需結構描述繫結函數的詳細資訊，請參閱[建立使用者定義函數 &#40;Database Engine&#41;](../user-defined-functions/create-user-defined-functions-database-engine.md)。  
  
## <a name="getting-information-about-synonyms"></a>取得同義字的相關資訊  
 Sys.synonyms 目錄檢視含有一個關於給定資料庫中各個同義字的項目。 此目錄檢視會公開同義字中繼資料，例如同義字的名稱與基底物件的名稱。 如需`sys.synonyms`目錄檢視的詳細資訊，請參閱[&#40;transact-sql&#41;的 sys.databases ](/sql/relational-databases/system-catalog-views/sys-synonyms-transact-sql)。  
  
 透過擴充屬性的運用，您可以將描述性或指示性文字、輸入遮罩以及格式化規則新增為同義字的屬性。 由於屬性儲存在資料庫中，因此讀取屬性的所有應用程式都能夠以同樣的方式評估物件。 如需詳細資訊，請參閱 [sp_addextendedproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql)。  
  
 若要尋找同義字基底物件的基底類型，請使用 OBJECTPROPERTYEX 函數。 如需詳細資訊，請參閱 [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/objectproperty-transact-sql)。  
  
### <a name="examples"></a>範例  
 以下範例將傳回屬於本機物件之同義字基底物件的基底類型。  
  
```  
USE tempdb;  
GO  
CREATE SYNONYM MyEmployee   
FOR AdventureWorks2012.HumanResources.Employee;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID('MyEmployee'), 'BaseType') AS BaseType;  
```  
  
 以下範例將傳回屬於遠端物件 (位於 `Server1`伺服器上) 之同義字基底物件的基底類型。  
  
```  
EXECUTE sp_addlinkedserver Server1;  
GO  
CREATE SYNONYM MyRemoteEmployee  
FOR Server1.AdventureWorks2012.HumanResources.Employee;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID('MyRemoteEmployee'), 'BaseType') AS BaseType;  
GO  
```  
  
## <a name="related-content"></a>相關內容  
 [建立同義字](create-synonyms.md)  
  
 [CREATE SYNONYM &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-synonym-transact-sql)  
  
 [DROP SYNONYM &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-synonym-transact-sql)  
  
  
