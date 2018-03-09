---
title: "sp_xml_removedocument (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_xml_removedocument_TSQL
- sp_xml_removedocument
dev_langs:
- TSQL
helpviewer_keywords:
- sp_xml_removedocument
ms.assetid: f9dca50a-8baf-4170-90bc-e72783ce5b73
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6eb570d1587b9f8826fee92d32c2f64828530679
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="spxmlremovedocument-transact-sql"></a>sp_xml_removedocument (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  移除由文件控制代碼所指定之 XML 文件的內部表示法，以及使該文件控制代碼失效。  
  
> [!NOTE]  
>  經過剖析的文件儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的內部快取中。 MSXML 剖析器 (Msxmlsql.dll) 會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 總記憶體的八分之一。 若要避免記憶體不足，請執行**sp_xml_removedocument**以釋出記憶體。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_xml_removedocument hdoc  
```  
  
## <a name="arguments"></a>引數  
 *hdoc*  
 這是新建立之文件的控制代碼。 無效的控制代碼會傳回錯誤。 *hdoc*是整數。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 >0 (失敗)  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會移除 XML 文件的內部表示法。 會提供文件的控制代碼作為輸入。  
  
```  
EXEC sp_xml_removedocument @hdoc;  
```  
  
## <a name="see-also"></a>請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [XML 預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/xml-stored-procedures-transact-sql.md)   
 [sp_xml_preparedocument &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xml-preparedocument-transact-sql.md)   
 [OPENXML &#40;Transact-SQL&#41;](../../t-sql/functions/openxml-transact-sql.md)  
  
  
