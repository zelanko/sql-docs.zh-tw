---
title: SET DELETED 命令 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 54900f00e03e1f236baf0b6eef152081b1f384a1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67997742"
---
# <a name="set-deleted-command"></a>SET DELETED 命令
指定是否標示為要刪除的記錄會被處理，以及是否可用於其他命令。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET DELETED ON | OFF  
```  
  
## <a name="arguments"></a>引數  
 ON  
 （預設驅動程式; Visual FoxPro 的預設值是 OFF）。指定的命令操作記錄 （包括相關資料表中的記錄） 上使用範圍忽略標示為要刪除的記錄。  
  
 OFF  
 指定的記錄標示為可存取刪除的記錄 （包括相關資料表中的記錄） 運作的命令使用範圍。  
  
## <a name="remarks"></a>備註  
 查詢可以使用 Visual FoxPro Rushmore 技術，如果資料表具有索引上已刪除 （） 進行最佳化使用已刪除 （） 來測試記錄的狀態。  
  
> [!IMPORTANT]  
>  如果此命令的預設範圍是目前的記錄，或包含範圍內的單一記錄，則會忽略設定刪除。 索引一律會忽略設定刪除，並編製索引的資料表中的所有記錄。  
  
## <a name="see-also"></a>另請參閱  
 [DELETE - SQL 命令](../../odbc/microsoft/delete-sql-command.md)
