---
title: Sp_helptrigger 輸出中的新資料行可能會影響應用程式 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- sp_helptrigger
ms.assetid: b7c42a8f-f2e0-4fa3-b046-3cf39c854c47
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2d62b9b9546fa113557bf962d68876d8c55a71ef
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032013"
---
# <a name="new-column-in-output-of-sphelptrigger-may-impact-applications"></a>sp_helptrigger 輸出中的新資料行，可能會影響應用程式
  trigger_schemaias 結果集的最後一個資料行傳回 sp_helptrigger 系統預存程序。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 若要取得針對特定資料表定義之觸發程序的相關資訊，請查詢 sys.triggers 目錄檢視。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>更正動作  
 請檢閱 sp_helptrigger 在應用程式中的使用方式。 您可能需要修改應用程式，以配合其他資料行。 或者，您也可以改用 sys.triggers 目錄檢視。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
