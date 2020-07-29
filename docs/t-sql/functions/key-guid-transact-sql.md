---
title: KEY_GUID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Key_GUID_TSQL
- Key_GUID
dev_langs:
- TSQL
helpviewer_keywords:
- symmetric keys [SQL Server], GUIDs
- KEY_GUID function
- GUIDs [SQL Server]
ms.assetid: 9246c7b2-7098-42c4-a222-cbf30267c46a
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 1fbddf97fc08ffe0b200b1affa7258cc2746e0ca
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87111941"
---
# <a name="key_guid-transact-sql"></a>KEY_GUID (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  傳回資料庫中對稱金鑰的 GUID。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
Key_GUID( 'Key_Name' )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 **'** *Key_Name* **'**  
 資料庫中的對稱金鑰名稱。  
  
## <a name="return-types"></a>傳回型別  
 **uniqueidentifier**  
  
## <a name="remarks"></a>備註  
 如果識別值是在建立金鑰時指定，則其 GUID 為該識別值的 MD5 雜湊。 如果未指定任何識別值，伺服器便會產生 GUID。  
  
 如果金鑰是一個暫時金鑰，則金鑰名稱必須以數字符號 (#) 開頭。  
  
## <a name="permissions"></a>權限  
 由於暫時金鑰只能用在建立它們的工作階段當中，因此存取它們無需任何權限。 若要存取非暫時的金鑰，呼叫端就必須對金鑰具備某種權限，而且絕對不能拒絕過該金鑰的 VIEW 權限。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 `ABerglundKey1` 對稱金鑰的 GUID。  
  
```  
SELECT Key_GUID('ABerglundKey1');  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [sys.symmetric_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [sys.key_encryptions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-key-encryptions-transact-sql.md)  
  
  
