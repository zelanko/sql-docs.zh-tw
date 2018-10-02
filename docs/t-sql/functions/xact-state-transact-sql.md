---
title: XACT_STATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- XACT_STATE
- XACT_STATE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- states [SQL Server], transactions
- uncommittable transactions
- sessions [SQL Server], active transactions
- XACT_STATE function
- transactions [SQL Server], state
- active transactions
ms.assetid: e9300827-e793-4eb6-9042-ffa0204aeb50
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d74e1ebfb3f1d8e2bc36c2a4bd0432a830934b5d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47799336"
---
# <a name="xactstate-transact-sql"></a>XACT_STATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  這是報告目前正在執行之要求的使用者交易狀態的純量函數。 XACT_STATE 指出要求是否具有使用中的使用者交易，以及是否可以認可該交易。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
XACT_STATE()  
```  
  
## <a name="return-type"></a>傳回類型  
 **smallint**  
  
## <a name="remarks"></a>Remarks  
 XACT_STATE 會傳回下列值。  
  
|傳回值|意義|  
|------------------|-------------|  
|1|目前的要求具有使用中的使用者交易。 要求可以執行任何動作，其中包括寫入資料和認可交易。|  
|0|目前的要求沒有任何使用中的使用者交易。|  
|-1|目前的要求有一項使用中的使用者交易，但發生錯誤，使交易被分類為無法認可的交易。 要求無法認可交易或回復到儲存點；它只能要求完整回復交易。 要求無法執行任何寫入作業，直到它回復交易為止。 要求只能執行讀取作業，直到它回復交易為止。 在交易回復之後，要求便可以執行讀取和寫入作業，且可以起始一項新交易。<br /><br /> 當最外層的批次完成執行時，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會自動回復任何使用中無法認可的交易。 如果在交易進入無法認可的狀態時沒有傳送任何錯誤訊息，則當批次完成時，就會將錯誤訊息傳送給用戶端應用程式。 此訊息表示偵測到無法認可的交易，並已回復。|  
  
 XACT_STATE 和 @@TRANCOUNT 函式都可用來偵測目前的要求是否有使用中的使用者交易。 @@TRANCOUNT 無法用來判斷交易是否已分類為無法認可的交易。 XACT_STATE 無法用來判斷是否有巢狀交易。  
  
## <a name="examples"></a>範例  
 下列範例會在 `XACT_STATE` 建構之 `CATCH` 區塊中使用 `TRY…CATCH`，來決定要認可或回復交易。 由於 `SET XACT_ABORT` 是 `ON`，因此，條件約束違規錯誤會使交易進入無法認可的狀態。  
  
```  
USE AdventureWorks2012;  
GO  
  
-- SET XACT_ABORT ON will render the transaction uncommittable  
-- when the constraint violation occurs.  
SET XACT_ABORT ON;  
  
BEGIN TRY  
    BEGIN TRANSACTION;  
        -- A FOREIGN KEY constraint exists on this table. This   
        -- statement will generate a constraint violation error.  
        DELETE FROM Production.Product  
            WHERE ProductID = 980;  
  
    -- If the delete operation succeeds, commit the transaction. The CATCH  
    -- block will not execute.  
    COMMIT TRANSACTION;  
END TRY  
BEGIN CATCH  
    -- Test XACT_STATE for 0, 1, or -1.  
    -- If 1, the transaction is committable.  
    -- If -1, the transaction is uncommittable and should   
    --     be rolled back.  
    -- XACT_STATE = 0 means there is no transaction and  
    --     a commit or rollback operation would generate an error.  
  
    -- Test whether the transaction is uncommittable.  
    IF (XACT_STATE()) = -1  
    BEGIN  
        PRINT 'The transaction is in an uncommittable state.' +  
              ' Rolling back transaction.'  
        ROLLBACK TRANSACTION;  
    END;  
  
    -- Test whether the transaction is active and valid.  
    IF (XACT_STATE()) = 1  
    BEGIN  
        PRINT 'The transaction is committable.' +   
              ' Committing transaction.'  
        COMMIT TRANSACTION;     
    END;  
END CATCH;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)   
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [SAVE TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/save-transaction-transact-sql.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)  
  
  
