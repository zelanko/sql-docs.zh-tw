---
title: 設定已刪除的命令 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300878"
---
# <a name="set-deleted-command"></a>SET DELETED 命令
指定是否處理標記為刪除的記錄，以及是否可在其他命令中使用它們。  
  
## <a name="syntax"></a>語法  
  
```  
  
SET DELETED ON | OFF  
```  
  
## <a name="arguments"></a>引數  
 開啟  
 （驅動程式的預設值; Visual FoxPro 的預設值為 OFF）。指定在記錄中操作的命令（包括相關資料表中的記錄），使用範圍忽略標記為刪除的記錄。  
  
 OFF  
 指定標記為刪除的記錄可以透過使用範圍的記錄（包括相關資料表中的記錄）來存取。  
  
## <a name="remarks"></a>備註  
 如果資料表在已刪除（）上編制索引，使用已刪除（）來測試記錄狀態的查詢可以使用 Visual FoxPro Rushmore 技術進行優化。  
  
> [!IMPORTANT]  
>  如果命令的預設範圍是目前的記錄，或如果您包含單一記錄的範圍，則會忽略 SET DELETED。 索引一律會忽略已刪除的集合，並為數據表中的所有記錄編制索引。  
  
## <a name="see-also"></a>另請參閱  
 [DELETE - SQL 命令](../../odbc/microsoft/delete-sql-command.md)
