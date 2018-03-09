---
title: "SET SHOWPLAN_XML (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET SHOWPLAN_XML
- SET_SHOWPLAN_XML_TSQL
dev_langs: TSQL
helpviewer_keywords:
- statements [SQL Server], estimates
- SET SHOWPLAN_XML statement
- execution information and estimates [SQL Server]
- statements [SQL Server], information without processing
- XML [SQL Server], statement execution information
- SHOWPLAN_XML option
- estimated execution information [SQL Server]
ms.assetid: a467a1b3-10a5-43c4-9085-13d8aed549c9
caps.latest.revision: "48"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: bd4e6309f65bea4a71cc9e2de7d5bb5b806ab005
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="set-showplanxml-transact-sql"></a>SET SHOWPLAN_XML (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 相反地，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會以妥善定義的 XML 文件格式來傳回有關如何執行這些陳述式的詳細資訊。  
 
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
SET SHOWPLAN_XML { ON | OFF }  
```  
  
## <a name="remarks"></a>備註  
 SET SHOWPLAN_XML 的設定是在執行階段進行設定，而不是在剖析階段進行設定。  
  
 當 SET SHOWPLAN_XML 是 ON，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]情況下，傳回每個陳述式的執行計畫資訊並[!INCLUDE[tsql](../../includes/tsql-md.md)]不執行陳述式。 在這個選項設為 ON 之後，會傳回所有後續 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的執行計畫相關資訊，直到這個選項設為 OFF 為止。 例如，如果執行 CREATE TABLE 陳述式時，SET SHOWPLAN_XML 是 ON，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會從包含這份相同資料表的後續 SELECT 陳述式傳回錯誤訊息；指定的資料表並不存在。 因此，後來參考這份資料表都會失敗。 當 SET SHOWPLAN_XML 是 OFF 時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在未產生報表的情況下，執行這些陳述式。  
  
 SET SHOWPLAN_XML 要傳回做為輸出**nvarchar （max)**之類的應用程式的**sqlcmd**公用程式，其中 XML 輸出後續可由其他工具來顯示和處理查詢計劃資訊。  
  
> [!NOTE]  
>  動態管理檢視， **sys.dm_exec_query_plan**，傳回 SET SHOWPLAN XML 中的相同資訊**xml**資料型別。 此資訊會從傳回**query_plan**資料行**sys.dm_exec_query_plan**。 如需詳細資訊，請參閱[sys.dm_exec_query_plan &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md).  
  
 在預存程序內，不能指定 SET SHOWPLAN_XML。 它必須是批次中的唯一陳述式。  
  
 SET SHOWPLAN_XML 會將資訊當作一組 XML 文件傳回。 SET SHOWPLAN_XML ON 陳述式之後的每個批次都會反映在單一文件的輸出中。 每份文件都包含批次內各陳述式的文字，後面接著執行步驟的詳細資料。 文件會顯示估計的成本、資料列數、存取的索引、執行的運算子類型、聯結順序，以及執行計畫的詳細資訊。  
  
 在安裝期間，會將包含 SET SHOWPLAN_XML 的 XML 輸出之 XML 結構描述的文件，複製到安裝了 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之電腦的本機目錄中。 您可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝檔所在的磁碟機中找到它，位置如下：  
  
 \Microsoft SQL Server\130\Tools\Binn\schemas\sqlserver\2004\07\showplan\showplanxml.xsd  
  
 顯示計畫結構描述也可以在找到[這個網站](http://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409)。  
  
> [!NOTE]  
>  如果**包括實際執行計畫**中選取[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，這個 SET 選項不會產生 XML 執行程序表輸出。 清除**包括實際執行計畫**按鈕才能使用這個 SET 選項。  
  
## <a name="permissions"></a>Permissions  
 若要使用 SET SHOWPLAN_XML，您必須有執行 SET SHOWPLAN_XML 所針對的陳述式之充份權限，且您必須有包含所參考物件的所有資料庫之 SHOWPLAN 權限。  
  
 如 SELECT、 INSERT、 UPDATE、 DELETE、 EXEC *stored_procedure*，和 EXEC *user_defined_function*陳述式，以產生顯示計畫，使用者必須：  
  
-   有執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的適當權限。  
  
-   有包含 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式所參考的物件 (如資料表、檢視等) 之所有資料庫的 SHOWPLAN 權限。  
  
 對於所有其他陳述式，例如 DDL、 USE *database_name*、 SET、 DECLARE、 動態 SQL，以及等等，只有適當的權限執行[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式所需。  
  
## <a name="examples"></a>範例  
 下面兩個陳述式利用 SET SHOWPLAN_XML 設定來顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分析和最佳化查詢中之索引使用情況的方式。  
  
 第一個查詢在索引資料行的 WHERE 子句中，使用等於比較運算子 (=)。 第二個查詢在 WHERE 子句中使用 LIKE 運算子。 這會強制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用叢集索引掃描，以及尋找符合 WHERE 子句條件的資料。 中的值**EstimateRows**和**EstimatedTotalSubtreeCost**屬性都是第一個索引查詢，指出它處理速度，並使用較少的資源比非索引查詢。  
  
```  
USE AdventureWorks2012;  
GO  
SET SHOWPLAN_XML ON;  
GO  
-- First query.  
SELECT BusinessEntityID   
FROM HumanResources.Employee  
WHERE NationalIDNumber = '509647174';  
GO  
-- Second query.  
SELECT BusinessEntityID, JobTitle  
FROM HumanResources.Employee  
WHERE JobTitle LIKE 'Production%';  
GO  
SET SHOWPLAN_XML OFF;  
```  
  
## <a name="see-also"></a>另請參閱  
 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
