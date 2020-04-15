---
title: 設定刪除命令 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET DELETED command [ODBC]
ms.assetid: 6b5e0086-156d-471d-8e7f-6c5fa9686cd5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3b3302dc7eecca7135dab9dff5afa376169be0f1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300878"
---
# <a name="set-deleted-command"></a>SET DELETED 命令
指定是否處理標記為刪除的記錄以及這些記錄是否可用於其他命令。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET DELETED ON | OFF  
```  
  
## <a name="arguments"></a>引數  
 開啟  
 (驅動程式的預設值;Visual FoxPro 的預設值為 OFF。指定使用作用域對記錄(包括相關表中的記錄)執行的命令忽略標記為要刪除的記錄。  
  
 OFF  
 指定標記為刪除的記錄可以通過使用作用域對記錄(包括相關表中的記錄)操作的命令進行訪問。  
  
## <a name="remarks"></a>備註  
 如果使用 DELETED( ) 測試記錄狀態的查詢,如果表在 DELETED() 上編製索引,則可以使用 Visual FoxPro Rushmore 技術進行優化。  
  
> [!IMPORTANT]  
>  如果命令的預設範圍是當前記錄,或者包含單個記錄的範圍,則忽略 SET DELETED。 INDEX 始終忽略"設置刪除"並索引表中的所有記錄。  
  
## <a name="see-also"></a>另請參閱  
 [DELETE - SQL 命令](../../odbc/microsoft/delete-sql-command.md)
