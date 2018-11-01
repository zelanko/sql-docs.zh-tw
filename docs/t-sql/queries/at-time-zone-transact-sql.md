---
title: AT TIME ZONE (Transact-SQL) | Microsoft Docs
ms.date: 11/16/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.custom: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- AT TIME ZONE
- AT_TIME_ZONE_TSQL
helpviewer_keywords:
- AT TIME ZONE function
ms.assetid: 311f682f-7f1b-43b6-9ea0-24e36b64f73a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 663733493bba7e96d8bb55519013128fd62a2eaf
ms.sourcegitcommit: 5d6e1c827752c3aa2d02c4c7653aefb2736fffc3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/10/2018
ms.locfileid: "49072232"
---
# <a name="at-time-zone-transact-sql"></a>AT TIME ZONE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  將 *inputdate* 轉換成目標時區中對應的 *datetimeoffset* 值。 如果提供 *inputdate* 但未提供位移資訊，此函數就會在假設目標時區中已提供 *inputdate* 值的情況下，套用時區位移。 如果提供 *inputdate* 來作為 *datetimeoffset* 值，則 **AT TIME ZONE** 子句會使用時區轉換規則來將它轉換成目標時區。  
  
 **AT TIME ZONE** 實作需倚賴 Windows 機制來跨時區轉換 **datetime** 值。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
inputdate AT TIME ZONE timezone  
```  
  
## <a name="arguments"></a>引數  
 *inputdate*  
 這是可解析成下列值的運算式：**smalldatetime**、**datetime**、**datetime2** 或 **datetimeoffset**。  
  
 *timezone*  
 目的地時區的名稱。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 需倚賴儲存在「Windows 登錄」中的時區。 安裝在電腦上的所有時區都儲存在下列登錄區中：**KEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zones**。 已安裝的時區清單也會透過 [sys.time_zone_info &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-time-zone-info-transact-sql.md) 檢視表公開。  
  
## <a name="return-types"></a>傳回類型  
 傳回 **datetimeoffset** 的資料類型  
  
## <a name="return-value"></a>傳回值  
 目標時區中的 **datetimeoffset** 值。  
  
## <a name="remarks"></a>Remarks  
 **AT TIME ZONE** 會針對 **smalldatetime**、**datetime** 及 **datetime2** 資料類型中，落在受 DST 變更影響之間隔內的輸入值，套用特定的轉換規則：  
  
-   將時鐘往前調整時，本地時間會有落差，其持續時間取決於時鐘調整的持續時間 (通常為 1 小時，但也可能是 30 或 45 分鐘，視時區而定)。 在此情況下，會使用在 DST 變更「之後」的位移來轉換屬於此落差的時間點。  
  
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
  
- 將時鐘調整回來時，2 個小時的本地時間就會重疊成 1 個小時。  在此情況下，會使用在時鐘變更「之前」的位移來顯示屬於重疊間隔的時間點：  
  
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

由於部分資訊 (例如時區規則) 的維護是在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 外部進行且可能偶爾會有變更，因此 **AT TIME ZONE** 函數被歸類為不具決定性的函數。 
  
## <a name="examples"></a>範例  
  
### <a name="a-add-target-time-zone-offset-to-datetime-without-offset-information"></a>A. 將目標時區位移新增至不含位移資訊的日期時間  
 當您知道在相同時區中已提供原始 **datetime** 值時，請使用 **AT TIME ZONE** 來根據時區規則新增位移：  
  
```  
USE AdventureWorks2016;  
GO  
  
SELECT SalesOrderID, OrderDate,   
    OrderDate AT TIME ZONE 'Pacific Standard Time' AS OrderDate_TimeZonePST  
FROM Sales.SalesOrderHeader;  
```  
  
### <a name="b-convert-values-between-different-time-zones"></a>B. 在不同的時區之間轉換值  
 下列範例會在不同的時區之間轉換值：  
  
```  
USE AdventureWorks2016;  
GO  
  
SELECT SalesOrderID, OrderDate,   
    OrderDate AT TIME ZONE 'Pacific Standard Time' AS OrderDate_TimeZonePST,  
    OrderDate AT TIME ZONE 'Pacific Standard Time'   
    AT TIME ZONE 'Central European Standard Time' AS OrderDate_TimeZoneCET  
FROM Sales.SalesOrderHeader;  
```  
  
### <a name="c-query-temporal-tables-using-local-time-zone"></a>C. 使用本地時區的查詢時態表  
 下列範例會從時態表選取資料。  
  
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
 [日期和時間資料類型與函數 &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)  
  
  
