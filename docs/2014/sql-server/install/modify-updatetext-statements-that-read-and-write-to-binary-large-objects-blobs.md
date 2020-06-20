---
title: 修改讀取和寫入二進位大型物件（Blob）的 UPDATETEXT 語句 |Microsoft Docs
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
ms.openlocfilehash: 061e7bad0bae5a74d103406265ad79195f79f7db
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059209"
---
# <a name="modify-updatetext-statements-that-read-and-write-to-binary-large-objects-blobs"></a>修改讀取和寫入二進位大型物件 (BLOB) 的 UPDATETEXT 陳述式
  Upgrade Advisor 偵測到使用相同文字指標來讀取和寫入相同二進位大型物件區塊 (BLOB) 的 UPDATETEXT 陳述式。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 不支援這樣使用文字指標。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>更正動作  
 將 BLOB 複製至暫存資料表或資料表變數，然後將值指派回原始資料行。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫引擎升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor &#91;新的&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
