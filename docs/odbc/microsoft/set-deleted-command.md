---
description: SET DELETED 命令
title: 設定刪除的命令 |Microsoft Docs
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
ms.openlocfilehash: 60e00af582e0440957c8a4e743624e00f0ba3e58
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466370"
---
# <a name="set-deleted-command"></a>SET DELETED 命令
指定是否處理標示為刪除的記錄，以及是否可在其他命令中使用它們。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET DELETED ON | OFF  
```  
  
## <a name="arguments"></a>引數  
 開啟  
 驅動程式 (預設值;Visual FoxPro 的預設值為 OFF。 ) 指定在記錄上操作的命令 (包括相關資料表中的記錄) 使用範圍略過標示為刪除的記錄。  
  
 OFF  
 指定針對記錄進行操作的命令可以存取標記為刪除的記錄， (包括) 使用範圍之相關資料表中的記錄。  
  
## <a name="remarks"></a>備註  
 如果資料表是在刪除的 ( ) 上編制索引，則使用 [已刪除的 (] ) 測試記錄狀態的查詢可以使用 Visual FoxPro Rushmore 技術進行優化。  
  
> [!IMPORTANT]  
>  如果命令的預設範圍是目前的記錄，或者您包含單一記錄的範圍，則會忽略 SET DELETED。 索引一律會忽略已刪除的集合，並為數據表中的所有記錄編制索引。  
  
## <a name="see-also"></a>另請參閱  
 [DELETE - SQL 命令](../../odbc/microsoft/delete-sql-command.md)
