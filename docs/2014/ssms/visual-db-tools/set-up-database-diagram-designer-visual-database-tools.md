---
title: 設定資料庫圖表設計工具 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.diagnostic.InstallSqlDiagramSupport
helpviewer_keywords:
- Database Diagram Designer
- database diagrams [SQL Server], Database Diagram Designer
- diagrams [SQL Server], Database Diagram Designer
ms.assetid: 927321ee-b459-4f5b-9719-4a7a95639143
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d71ea2d6a10755ef52e0cac37ddcd2385d82d9cb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63067609"
---
# <a name="set-up-database-diagram-designer-visual-database-tools"></a>設定資料庫圖表設計工具 (Visual Database Tools)
  若要使用資料庫圖表設計工具，必須先由 **db_owner** 角色的成員進行設定，才能控制圖表的存取權。  
  
### <a name="to-set-up-database-diagramming"></a>設定資料庫圖表化  
  
1.  從 [物件總管] 中，展開資料庫節點。  
  
2.  在資料庫連接中展開 [資料庫圖表] 節點。  
  
3.  如果您要設定資料庫圖表化，可在提示出現時選取 [是]  。  
  
    > [!NOTE]  
    >  這會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中建立資料庫圖表資料表、系統預存程序和系統函數。  
  
4.  Visual Studio 會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體上建立下列物件：  
  
    1.  sysdiagrams 資料表  
  
    2.  sp_alterdiagram 預存程序  
  
    3.  sp_creatediagram 預存程序  
  
    4.  sp_dropdiagram 預存程序  
  
    5.  sp_renamediagram 預存程序  
  
    6.  fn_diagramobjects 函數  
  
    7.  sp_helpdiagrams 預存程序  
  
    8.  sp_helpdiagramsdefinition 預存程序  
  
    9. sp_upgraddiagrams 預存程序  
  
## <a name="see-also"></a>另請參閱  
 [瞭解資料庫關係圖擁有權 &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [升級舊版的資料庫關係圖 &#40;Visual Database Tools&#41;](upgrade-database-diagrams-from-previous-editions-visual-database-tools.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-authorization-transact-sql)  
  
  
