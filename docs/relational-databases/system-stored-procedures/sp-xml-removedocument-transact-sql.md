---
title: sp_xml_removedocument （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_xml_removedocument_TSQL
- sp_xml_removedocument
dev_langs:
- TSQL
helpviewer_keywords:
- sp_xml_removedocument
ms.assetid: f9dca50a-8baf-4170-90bc-e72783ce5b73
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6219f18bee08d5c20431cb87a2cb30795c515d7a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67950477"
---
# <a name="sp_xml_removedocument-transact-sql"></a>sp_xml_removedocument (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  移除由文件控制代碼所指定之 XML 文件的內部表示法，以及使該文件控制代碼失效。  
  
> [!NOTE]  
>  經過剖析的文件儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的內部快取中。 MSXML 剖析器 (Msxmlsql.dll) 會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 總記憶體的八分之一。 若要避免記憶體不足，請執行**sp_xml_removedocument**以釋放記憶體。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_xml_removedocument hdoc  
```  
  
## <a name="arguments"></a>引數  
 *hdoc*  
 這是新建立之文件的控制代碼。 無效的控制代碼會傳回錯誤。 *hdoc*是整數。  
  
## <a name="return-code-values"></a>傳回碼值  
 0（成功）或 >0 （失敗）  
  
## <a name="permissions"></a>權限  
 需要 **public** 角色的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會移除 XML 文件的內部表示法。 會提供文件的控制代碼作為輸入。  
  
```  
EXEC sp_xml_removedocument @hdoc;  
```  
  
## <a name="see-also"></a>另請參閱      
 <br>[系統預存程式（Transact-sql）](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)
 <br>[XML 預存程式（Transact-sql）](../../relational-databases/system-stored-procedures/xml-stored-procedures-transact-sql.md)
 <br>[sys.databases dm_exec_xml_handles （Transact-sql）](../system-dynamic-management-views/sys-dm-exec-xml-handles-transact-sql.md)
 <br>[sp_xml_preparedocument （Transact-sql）](../../relational-databases/system-stored-procedures/sp-xml-preparedocument-transact-sql.md)
 <br>[OPENXML (Transact-SQL)](../../t-sql/functions/openxml-transact-sql.md)
  
  
