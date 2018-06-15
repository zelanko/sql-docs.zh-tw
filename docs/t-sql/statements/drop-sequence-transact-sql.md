---
title: DROP SEQUENCE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DROP SEQUENCE
- DROP_SEQUENCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP SEQUENCE statement
- sequence number object, dropping
ms.assetid: c25772d3-61af-4aa7-b58b-a6f67a793e3d
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 1db38ddb9a68f078bc369b06fcd9814270a4ab9d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33066655"
---
# <a name="drop-sequence-transact-sql"></a>DROP SEQUENCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  從目前資料庫移除順序物件。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
DROP SEQUENCE [ IF EXISTS ] { [ database_name . [ schema_name ] . | schema_name. ]    sequence_name } [ ,...n ]  
 [ ; ]  
```  
  
## <a name="arguments"></a>引數  
 *IF EXISTS*  
 **適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。  
  
 只有在序列已存在時，才能有條件地將其卸除。  
  
 *database_name*  
 這是建立順序物件的資料庫名稱。  
  
 *schema_name*  
 這是順序物件所屬的結構描述名稱。  
  
 *sequence_name*  
 這是要卸除的順序名稱。 類型是 **sysname**。  
  
## <a name="remarks"></a>Remarks  
 在產生數字之後，順序物件與所產生的數字沒有持續的關聯性，因此即使產生的數字仍在使用中，也可以卸除順序數字。  
  
 因為順序物件不是結構描述繫結，即使由預存程序或觸發程序參考時，也可以卸除順序物件。 如果當做資料表中的預設值來參考，便無法卸除順序物件。 錯誤訊息會列出參考順序的物件。  
  
 若要列出資料庫中的所有順序物件，請執行下列陳述式。  
  
```  
SELECT sch.name + '.' + seq.name AS [Sequence schema and name]   
    FROM sys.sequences AS seq  
    JOIN sys.schemas AS sch  
        ON seq.schema_id = sch.schema_id ;  
GO  
```  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Permissions  
 需要結構描述的 ALTER 或 CONTROL 權限。  
  
### <a name="audit"></a>稽核  
 若要稽核 **DROP SEQUENCE**，請監視 **SCHEMA_OBJECT_CHANGE_GROUP**。  
  
## <a name="examples"></a>範例  
 下列範例會從目前資料庫移除名稱為 `CountBy1` 的順序物件。  
  
```  
DROP SEQUENCE CountBy1 ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [NEXT VALUE FOR &#40;Transact-SQL&#41;](../../t-sql/functions/next-value-for-transact-sql.md)   
 [序號](../../relational-databases/sequence-numbers/sequence-numbers.md)  
  
  
