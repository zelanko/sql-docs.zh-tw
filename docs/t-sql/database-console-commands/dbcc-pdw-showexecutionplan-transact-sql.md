---
title: "DBCC PDW_SHOWEXECUTIONPLAN (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.service: sql-data-warehouse
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
caps.latest.revision: 12
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 461ee87f41692172b31125e36553c0eab0b09772
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-pdwshowexecutionplan-transact-sql"></a>DBCC PDW_SHOWEXECUTIONPLAN (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

顯示[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行在特定的查詢執行計畫[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]計算節點或控制節點。 使用此運算節點和控制節點上執行查詢時，進行查詢效能問題的疑難排解。
  
一旦可了解 SMP 的查詢效能問題[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]運算節點上執行的查詢有許多種，以改善效能。 可能的方式，來改善查詢效能的計算節點上包括建立多重資料行統計資料、 建立非叢集索引，或使用查詢提示。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [TRANSACT-SQL 語法慣例 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
SQL Server 的語法：

```sql
DBCC PDW_SHOWEXECUTIONPLAN ( distribution_id, spid )  
[;]  
```  
語法 Azure 平行資料倉儲：
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( pdw_node_id, spid )  
[;]  
```  
  
## <a name="arguments"></a>引數  
 *distribution_id*  
 執行查詢計劃發佈的識別項。 這是一個整數，而不能是 NULL。 使用為目標時[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。  
  
 *pdw_node_id*  
 正在執行的查詢計畫節點識別碼。 這是一個整數，而不能是 NULL。 應用裝置為目標時使用。  
  
 *spid*  
 識別項[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在執行的查詢計劃的工作階段。 這是一個整數，而不能是 NULL。  
  
## <a name="permissions"></a>Permissions  
 需要 CONTROL 權限的[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。  
  
需要 VIEW SERVER STATE 權限的應用裝置上。
  
## <a name="examples-includesssdwincludessssdw-mdmd"></a>範例：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]  
  
### <a name="a-dbcc-pdwshowexecutionplan-basic-syntax"></a>A. DBCC PDW_SHOWEXECUTIONPLAN 基本語法  
 在執行時[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]執行個體，請修改上述查詢，也選取 distribution_id。  
  
```sql
SELECT [sql_spid], [pdw_node_id], [request_id], [dms_step_index], [type], [start_time], [end_time], [status], [distribution_id]  
FROM sys.dm_pdw_dms_workers   
WHERE [status] <> 'StepComplete' and [status] <> 'StepError'  
order by request_id, [dms_step_index];  
```  
  
這會傳回每個正在執行的散發的 spid。 如果您對於 375 工作階段中執行何種散發 1 好奇，您可以執行下列的命令。
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( 1, 375 );  
```  

## <a name="examples-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="b-dbcc-pdwshowexecutionplan-basic-syntax"></a>B. DBCC PDW_SHOWEXECUTIONPLAN 基本語法  
 執行太長的查詢是執行 DMS 查詢計劃或 SQL 查詢計劃作業。  
  
如果查詢正在執行 DMS 查詢計劃作業，您可以使用下列查詢來擷取節點識別碼，而且未完成的步驟執行的工作階段識別碼的清單。
  
```sql
SELECT [sql_spid], [pdw_node_id], [request_id], [dms_step_index], [type], [start_time], [end_time], [status]   
FROM sys.dm_pdw_dms_workers   
WHERE [status] <> 'StepComplete' and [status] <> 'StepError'  
AND pdw_node_id = 201001   
order by request_id, [dms_step_index], [distribution_id];  
```  
  
根據先前查詢的結果，做為參數，DBCC PDW_SHOWEXEUCTIONPLAN 使用 sql_spid 和 pdw_node_id。 例如，下列命令會顯示 pdw_node_id 201001 和 sql_spid 375 的執行計畫。
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( 201001, 375 );  
```  

## <a name="see-also"></a>另請參閱
[DBCC PDW_SHOWPARTITIONSTATS &#40;TRANSACT-SQL &#41;](dbcc-pdw-showpartitionstats-transact-sql.md)  
[DBCC PDW_SHOWSPACEUSED &#40;TRANSACT-SQL &#41;](dbcc-pdw-showspaceused-transact-sql.md)
