---
title: 了解資料庫圖表擁有權 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.diagnostic.CannotOpenWithInvalidOwner
helpviewer_keywords:
- diagrams [SQL Server], ownership
- database diagrams [SQL Server], ownership
- owners [SQL Server], database diagrams
ms.assetid: 4a27a48e-c4ef-4017-82b8-0cac4d0bbcac
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: c2edc1df3be09bcf4bd957ef2ecc743f1cb3c75c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65098543"
---
# <a name="understand-database-diagram-ownership-visual-database-tools"></a>了解資料庫圖表擁有權 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
若要使用資料庫圖表設計工具，必須先由 db_owner 角色 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的角色) 的成員進行設定，才能控制圖表的存取權。 每個圖表必定有一個，也只能有一個擁有者，也就是建立該圖表的使用者。 如需設定圖表化的詳細資訊，請參閱 [設定資料庫圖表設計工具 (Visual Database Tools)](../../ssms/visual-db-tools/set-up-database-diagram-designer-visual-database-tools.md)。  
  
圖表擁有權有下列幾點注意事項：  
  
-   雖然任何有資料庫存取權的使用者都能建立圖表，但圖表建立後，則只有圖表的建立者及 db_owner 角色的任何成員可以檢視該圖表。  
  
-   圖表的擁有權只能轉移給 db_owner 角色的成員。 只有在圖表的先前擁有者已從資料庫中移除時，才能轉移擁有權。  
  
-   如果圖表擁有人已從資料庫中移除，圖表將保留在資料庫中，直到 db_owner 角色的成員開啟為止。 此時，db_owner 成員可選擇接管圖表的擁有權。  
  
## <a name="see-also"></a>另請參閱  
[使用資料庫圖表 (Visual Database Tools)](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
[設定資料庫圖表設計工具 (Visual Database Tools)](../../ssms/visual-db-tools/set-up-database-diagram-designer-visual-database-tools.md)  
  
