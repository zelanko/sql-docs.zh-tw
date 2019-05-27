---
title: 修改讀取和寫入二進位大型物件 (Blob) 的 UPDATETEXT 陳述式 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- UPDATETEXT statement
- text [SQL Server], UPDATETEXT statements
ms.assetid: b85da6a7-42f6-4707-a25e-3ded8958b94f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f2f3c8af333cc20398e7951bd6fd53433da0288c
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66093765"
---
# <a name="modify-updatetext-statements-that-read-and-write-to-binary-large-objects-blobs"></a>修改讀取和寫入二進位大型物件 (BLOB) 的 UPDATETEXT 陳述式
  Upgrade Advisor 偵測到使用相同文字指標來讀取和寫入相同二進位大型物件區塊 (BLOB) 的 UPDATETEXT 陳述式。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 不支援這樣使用文字指標。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>更正動作  
 將 BLOB 複製至暫存資料表或資料表變數，然後將值指派回原始資料行。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新增&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
