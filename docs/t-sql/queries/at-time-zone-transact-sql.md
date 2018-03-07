---
title: "時區 (TRANSACT-SQL) |Microsoft 文件"
ms.date: 11/16/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- AT TIME ZONE
- AT_TIME_ZONE_TSQL
helpviewer_keywords:
- AT TIME ZONE function
ms.assetid: 311f682f-7f1b-43b6-9ea0-24e36b64f73a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 8b77aeb47515f4140f78a70288e9e25d2acc52d1
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="at-time-zone-transact-sql"></a>時區 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  將轉換*inputdate*對應*datetimeoffset*目標時區中的值。 如果*inputdate*提供不含時差的資訊函式適用於假設的時區位移*inputdate*目標時區中提供值。 如果*inputdate*依現狀*datetimeoffset*值，比**AT TIME ZONE**子句將其轉換成使用時區轉換規則的目標時區。  
  
 **時區**實作依賴要轉換的 Windows 機制**datetime**跨時區的值。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
inputdate AT TIME ZONE timezone  
```  
  
## <a name="arguments"></a>引數  
 *inputdate*  
 運算式是可解析成**smalldatetime**， **datetime**， **datetime2**，或**datetimeoffset**值。  
  
 *timezone*  
 目的地時區的名稱。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]依賴 Windows 登錄中儲存的時區。 在電腦上安裝所有的時區會儲存在下列的登錄 hive: **KEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time 區域**。 一份已安裝的時區也會公開透過[sys.time_zone_info &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-time-zone-info-transact-sql.md)檢視。  
  
## <a name="return-types"></a>傳回類型  
 傳回的資料型別**datetimeoffset**  
  
## <a name="return-value"></a>傳回值  
 **Datetimeoffset**目標時區中的值。  
  
## <a name="remarks"></a>備註  
 **時區**適用於轉換中的輸入的值的特定規則**smalldatetime**， **datetime**和**datetime2**屬於資料型別受影響的間隔 DST 變更：  
  
-   當以本地時間的持續時間取決於時鐘調整的持續時間的差距就繼續設定時鐘 （通常是 1 小時，但它可以是 30 個或 45 分鐘，視時區而定）。 在此情況下，屬於此間隔時間點會轉換具有位移*之後*DST 變更。  
  
    ```  
    /*  
        Moving to DST in "Central European Standard Time" zone: 
        offset changes from +01:00 -> +02:00   
        Change occurred on March 29th, 2015 at 02:00:00.   
        Adjusted local time became 2015-03-29 03:00:00.  
    */  
    
    --Time before DST change has standard time offset (+01:00)
    SELECT CONVERT(datetime2(0), '2015-03-29T01:01:00', 126)     
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-03-29 01:01:00 +01:00   
  
    /*
      Adjusted time from the "gap interval" (between 02:00 and 03:00)
      is moved 1 hour ahead and presented with the summer time offset
      (after the DST change) 
    */
    SELECT CONVERT(datetime2(0), '2015-03-29T02:01:00', 126)   
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-03-29 03:01:00 +02:00
      
    --Time after 03:00 is presented with the summer time offset (+02:00)
    SELECT CONVERT(datetime2(0), '2015-03-29T03:01:00', 126)   
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-03-29 03:01:00 +02:00  
  
    ```  
  
- 當重設時鐘時，2 小時的本機時間會重疊到一小時。  在此情況下，屬於重疊的間隔時間點會有的位移*之前*時鐘變更：  
  
    ```  
    /*  
        Moving back from DST to standard time in 
        "Central European Standard Time" zone: 
        offset changes from +02:00 -> +01:00.  
        Change occurred on October 25th, 2015 at 03:00:00.   
        Adjusted local time became 2015-10-25 02:00:00   
    */  
    
    --Time before the change has DST offset (+02:00)
    SELECT CONVERT(datetime2(0), '2015-10-25T01:01:00', 126)      
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-10-25 01:01:00 +02:00  
    
    /*
      Time from the "overlapped interval" is presented with standard time 
      offset (before the change)    
    */
    SELECT CONVERT(datetime2(0), '2015-10-25T02:00:00', 126)   
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-10-25 02:00:00 +02:00  
    
    
    --Time after 03:00 is regularly presented with the standard time offset (+01:00)    
    SELECT CONVERT(datetime2(0), '2015-10-25T03:01:00', 126)   
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-10-25 03:01:00 +01:00
  
    ```  

因為某些資訊 （例如時區規則） 之外的維護[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]和可能會偶爾變動**AT TIME ZONE**函式類別，不具決定性。 
  
## <a name="examples"></a>範例  
  
### <a name="a-add-target-time-zone-offset-to-datetime-without-offset-information"></a>A. 加入不含位移資訊的日期時間的目標時區位移  
 使用**AT TIME ZONE**以時區規則時，您已了解的位移，將原始**datetime**提供相同的時區中的值：  
  
```  
USE AdventureWorks2016;  
GO  
  
SELECT SalesOrderID, OrderDate,   
    OrderDate AT TIME ZONE 'Pacific Standard Time' AS OrderDate_TimeZonePST  
FROM Sales.SalesOrderHeader;  
```  
  
### <a name="b-convert-values-between-different-time-zones"></a>B. 轉換不同的時區之間的值  
 下列範例會將轉換不同的時區之間的值：  
  
```  
USE AdventureWorks2016;  
GO  
  
SELECT SalesOrderID, OrderDate,   
    OrderDate AT TIME ZONE 'Pacific Standard Time' AS OrderDate_TimeZonePST,  
    OrderDate AT TIME ZONE 'Pacific Standard Time'   
    AT TIME ZONE 'Central European Standard Time' AS OrderDate_TimeZoneCET  
FROM Sales.SalesOrderHeader;  
```  
  
### <a name="c-query-temporal-tables-using-local-time-zone"></a>C. 查詢使用本地時區的時態表  
 下列範例會選取時態表中的資料。  
  
```  
USE AdventureWorks2016;  
GO  
  
DECLARE @ASOF datetimeoffset;  
SET @ASOF = DATEADD (month, -1, GETDATE()) AT TIME ZONE 'UTC';  
  
-- Query state of the table a month ago projecting period   
-- columns as Pacific Standard Time  
SELECT BusinessEntityID, PersonType, NameStyle, Title,   
    FirstName, MiddleName,  
    ValidFrom AT TIME ZONE 'Pacific Standard Time' 
FROM  Person.Person_Temporal  
FOR SYSTEM_TIME AS OF @ASOF;  
```  
  
## <a name="see-also"></a>另請參閱  
 [日期和時間類型](../../t-sql/data-types/date-and-time-types.md)   
 [日期和時間資料類型和函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)  
  
  
