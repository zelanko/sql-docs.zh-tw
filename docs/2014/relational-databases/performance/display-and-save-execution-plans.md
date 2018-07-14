---
title: 顯示並儲存執行計畫 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Showplan results
- execution plans [SQL Server]
- queries [SQL Server], tuning
- execution plans [SQL Server], how-to topics
- SQL Server Management Studio [SQL Server], execution plans
- tuning queries [SQL Server]
ms.assetid: bcd6f094-c613-4835-ae19-4caaadb4bb17
caps.latest.revision: 23
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f79a2ca73167d7db73628390eb114b7f4a58ecb3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37217090"
---
# <a name="display-and-save-execution-plans"></a>顯示並儲存執行計畫
  本節將說明如何顯示執行計畫，以及如何使用 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]將執行計畫儲存到 XML 格式的檔案中。  
  
 執行計畫會以圖形化的方式，顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查詢最佳化工具所選擇的資料擷取方法。 執行計畫會使用圖示來呈現 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中特定陳述式與查詢的執行成本，而不是使用 SET SHOWPLAN_ALL 或 SET SHOWPLAN_TEXT 陳述式所產生的表格呈現方式。 這種圖形式的方法，對於了解查詢的效能特性非常有幫助。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [顯示估計的執行計畫](display-the-estimated-execution-plan.md)  
  
-   [顯示實際執行計畫](display-an-actual-execution-plan.md)  
  
-   [以 XML 格式儲存執行計畫](save-an-execution-plan-in-xml-format.md)  
  
  
