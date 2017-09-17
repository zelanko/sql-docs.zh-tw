---
title: "SET 刪除命令 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SET DELETED command [ODBC]
ms.assetid: 6b5e0086-156d-471d-8e7f-6c5fa9686cd5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f3bf1ec522bee6fda19349a71c894ebd98bd75b9
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="set-deleted-command"></a>SET 刪除命令
指定是否標示為刪除的記錄會被處理，以及是否可用於其他命令。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET DELETED ON | OFF  
```  
  
## <a name="arguments"></a>引數  
 ON  
 （預設的驅動程式，Visual FoxPro 的預設值是 OFF）。指定之命令的作業記錄 （包括相關資料表中的記錄） 上使用範圍忽略標示為刪除的記錄。  
  
 OFF  
 指定的記錄標示為刪除可存取的記錄 （包括相關資料表中的記錄） 運作的命令所使用的範圍。  
  
## <a name="remarks"></a>備註  
 查詢可以使用 Visual FoxPro Rushmore 技術，如果資料表具有索引上已刪除 （） 可最佳化使用已刪除 （） 來測試記錄的狀態。  
  
> [!IMPORTANT]  
>  如果命令的預設範圍是目前的記錄，或包含單一記錄的範圍，則會忽略設定刪除。 索引一律會忽略設定刪除，並將索引資料表中的所有記錄。  
  
## <a name="see-also"></a>另請參閱  
 [刪除 SQL 命令](../../odbc/microsoft/delete-sql-command.md)
