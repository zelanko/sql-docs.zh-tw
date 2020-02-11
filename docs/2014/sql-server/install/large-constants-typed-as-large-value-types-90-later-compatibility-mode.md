---
title: 在90或更新版本的相容性模式中，大型常數的類型為大數數值型別 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- binary constants
- CHARINDEX function
- constants
- character string constants
- PATINDEX function
ms.assetid: 6e309fa0-5fb9-45a1-9739-f13fae525bfe
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8c7aded5577e28d94f42e108e46bb8a9c3cd6020
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66094085"
---
# <a name="large-constants-are-typed-as-large-value-types-in-90-or-later-compatibility-modes"></a>在 90 或之後的相容性模式中，大型常數的類型為大型數值類型
  Upgrade Advisor 偵測到大型常數的存在。 在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 中，大小超過 8,000 個位元組的字元字串常數和二進位常數會被視為大型物件資料類型。 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更新版本中，大型字元、Unicode 和二進位常數的類型是大型數值類型。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 當字串函數 (例如 CHARINDEX 和 PATINDEX) 與超過 8,000 個位元組的字串或二進位常數搭配使用時，[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 會傳回錯誤號碼 8116，而 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 會傳回錯誤號碼 8152。  
  
 在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 中，當字串函數與 `text`、`ntext` 和 `image` 資料類型搭配使用時，會傳回錯誤 8116。  
  
 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更新版本中，大型常數會分別被視為 `varchar(max)`、`nvarchar(max)` 和 `varbinary(max)` 資料類型。 這些資料類型與字串函數相容。  
  
 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更新版本中，字串函數 (例如 CHARINDEX 和 PATINDEX) 會假設包含要尋找之字元序列的字串小於 8,000 個位元組， 這就是為何會針對 CHARINDEX 和 PATINDEX 引發錯誤 8152。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫引擎升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor &#91;新的&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
