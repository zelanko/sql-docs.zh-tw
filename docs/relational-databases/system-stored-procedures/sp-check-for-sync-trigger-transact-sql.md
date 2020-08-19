---
description: sp_check_for_sync_trigger (Transact-SQL)
title: sp_check_for_sync_trigger (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- filter_TSQL
- sp_check_for_sync_trigger
helpviewer_keywords:
- sp_check_for_sync_trigger
ms.assetid: 54a1e2fd-c40a-43d4-ac64-baed28ae4637
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1e55fd24c9d4df46cb4703af31d2eda802a458ca
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88486204"
---
# <a name="sp_check_for_sync_trigger-transact-sql"></a>sp_check_for_sync_trigger (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  決定是否要在立即更新訂閱所使用的複寫觸發程序內容中呼叫使用者自訂觸發程序或是預存程序。 這個預存程序執行於發行集資料庫的發行者端，或訂閱資料庫的訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_check_for_sync_trigger [ @tabid = ] 'tabid'   
    [ , [ @trigger_op = ] 'trigger_output_parameters' OUTPUT ]  
    [ , [ @fonpublisher = ] fonpublisher ]  
```  
  
## <a name="arguments"></a>引數  
 [** @tabid =** ] '*tabid*'  
 這是要檢查立即更新觸發程序之資料表的物件識別碼。 *tabid* 是 **int** ，沒有預設值。  
  
 [** @trigger_op =** ] '*trigger_output_parameters*' 輸出  
 指定輸出參數是否要傳回呼叫它之觸發程序的類型。 *trigger_output_parameters* 是 **char (10) ** 且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**.Ins**|INSERT 觸發程序|  
|**Upd**|UPDATE 觸發程序|  
|**戴爾**|DELETE 觸發程序|  
|NULL (預設值)||  
  
`[ @fonpublisher = ] fonpublisher` 指定執行預存程式的位置。 *fonpublisher* 是 **bit**，預設值是0。 如果為 0，則是在訂閱者端執行，如果為 1，則是在發行者端執行。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 表示並非在立即更新觸發程序的內容中呼叫預存程序。 1表示它是在立即更新觸發程式的內容中進行呼叫，而且是* \@ trigger_op*中所傳回的觸發程式類型。  
  
## <a name="remarks"></a>備註  
 **sp_check_for_sync_trigger** 用於快照式複寫和異動複寫中。  
  
 **sp_check_for_sync_trigger** 是用來協調複寫和使用者定義的觸發程式。 這個預存程序會判斷它是否在複寫觸發程序內容之內受到呼叫。 例如，您可以在使用者定義的觸發程式主體中呼叫程式 **sp_check_for_sync_trigger** 。 如果 **sp_check_for_sync_trigger** 傳回 **0**，則使用者定義的觸發程式會繼續處理。 如果 **sp_check_for_sync_trigger** 傳回 **1**，則使用者定義的觸發程式會結束。 這可以確定當複寫觸發程序更新資料表時，不會引發使用者自訂觸發程序。  
  
## <a name="example"></a>範例  
 下列範例會顯示可用於訂閱者資料表之觸發程序中的程式碼。  
  
```  
DECLARE @retcode int, @trigger_op char(10), @table_id int  
SELECT @table_id = object_id('tablename')  
EXEC @retcode = sp_check_for_sync_trigger @table_id, @trigger_op OUTPUT  
IF @retcode = 1  
RETURN  
```  
  
## <a name="example"></a>範例  
 您也可以將程式碼加入至發行者端資料表的觸發程式。程式碼很類似，但 **sp_check_for_sync_trigger** 的呼叫包含額外的參數。  
  
```  
DECLARE @retcode int, @trigger_op char(10), @table_id int, @fonpublisher int  
SELECT @table_id = object_id('tablename')  
SELECT @fonpublisher = 1  
EXEC @retcode = sp_check_for_sync_trigger @table_id, @trigger_op OUTPUT, @fonpublisher  
IF @retcode = 1  
RETURN  
```  
  
## <a name="permissions"></a>權限  
 在[sys. objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)系統檢視中具有 SELECT 許可權的任何使用者都可以執行**sp_check_for_sync_trigger**預存程式。  
  
## <a name="see-also"></a>另請參閱  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
