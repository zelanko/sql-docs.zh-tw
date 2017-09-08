---
title: "KEY_GUID (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3e167366e86cf10403abc6cafa894ad964c60733
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="keyguid-transact-sql"></a>KEY_GUID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回資料庫中對稱金鑰的 GUID。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
Key_GUID( 'Key_Name' )  
```  
  
## <a name="arguments"></a>引數  
 **'** *Key_Name* **'**  
 資料庫中的對稱金鑰名稱。  
  
## <a name="return-types"></a>傳回類型  
 **uniqueidentifier**  
  
## <a name="remarks"></a>備註  
 如果識別值是在建立金鑰時指定，則其 GUID 為該識別值的 MD5 雜湊。 如果未指定任何識別值，伺服器便會產生 GUID。  
  
 如果金鑰是一個暫時金鑰，則金鑰名稱必須以數字符號 (#) 開頭。  
  
## <a name="permissions"></a>Permissions  
 由於暫時金鑰只能用在建立它們的工作階段當中，因此存取它們無需任何權限。 若要存取非暫時的金鑰，呼叫端就必須對金鑰具備某種權限，而且絕對不能拒絕過該金鑰的 VIEW 權限。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 `ABerglundKey1` 對稱金鑰的 GUID。  
  
```  
SELECT Key_GUID('ABerglundKey1');  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [sys.symmetric_keys &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [sys.key_encryptions &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-key-encryptions-transact-sql.md)  
  
  
