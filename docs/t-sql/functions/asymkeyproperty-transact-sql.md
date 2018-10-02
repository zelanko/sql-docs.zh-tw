---
title: ASYMKEYPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ASYMKEYPROPERTY_TSQL
- ASYMKEYPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- ASYMKEYPROPERTY
ms.assetid: a30581f2-e1b1-4996-93e6-527ff96b7c42
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dadfaeaf4debeba4b2da3f478b31fcb9bd5d3b67
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47664107"
---
# <a name="asymkeyproperty-transact-sql"></a>ASYMKEYPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

此函數傳回非對稱金鑰的屬性。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
ASYMKEYPROPERTY (Key_ID , 'algorithm_desc' | 'string_sid' | 'sid')  
```  
  
## <a name="arguments"></a>引數  
*Key_ID*  
資料庫中非對稱金鑰的 Key_ID。 如果您只知道金鑰名稱，請使用 ASYMKEY_ID 來尋找 Key_ID。 *Key_ID* 的資料型別為 **int**。
  
**'** algorithm_desc **'**  
指定輸出會傳回非對稱金鑰的演算法描述。 僅適用於根據 EKM 模組所建立的非對稱金鑰。
  
**'** string_sid **'**  
指定輸出以 **nvarchar()** 格式傳回非對稱金鑰的 SID。
  
**'** sid **'**  
指定輸出會以二進位格式傳回非對稱金鑰的 SID。
  
## <a name="return-types"></a>傳回類型  
**sql_variant**
  
## <a name="permissions"></a>[權限]  
需要非對稱金鑰上適當的權限，且呼叫端尚未拒絕非對稱金鑰的 VIEW 權限。 如需非對稱金鑰權限的詳細資訊，請參閱 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41; ](../../t-sql/statements/create-asymmetric-key-transact-sql.md)。
  
## <a name="examples"></a>範例  
下列範例傳回 Key_ID 256 的非對稱金鑰屬性。
  
```sql
SELECT   
ASYMKEYPROPERTY(256, 'algorithm_desc') AS Algorithm,  
ASYMKEYPROPERTY(256, 'string_sid') AS String_SID,  
ASYMKEYPROPERTY(256, 'sid') AS SID ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱
[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
[ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)  
[DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)  
[SIGNBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/signbyasymkey-transact-sql.md)  
[VERIFYSIGNEDBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/verifysignedbyasymkey-transact-sql.md)  
[加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
[sys.asymmetric_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-asymmetric-keys-transact-sql.md)  
[安全性目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)  
[ASYMKEY_ID &#40;Transact-SQL&#41;](../../t-sql/functions/asymkey-id-transact-sql.md)  
[SYMKEYPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/symkeyproperty-transact-sql.md)
  
  
