---
title: Sp_helptrigger 輸出中的新資料行可能會影響應用程式 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- sp_helptrigger
ms.assetid: b7c42a8f-f2e0-4fa3-b046-3cf39c854c47
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 0b1f5e936843ed84a5c6b88e2f3685e7a4272bc2
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85012165"
---
# <a name="new-column-in-output-of-sp_helptrigger-may-impact-applications"></a>sp_helptrigger 輸出中的新資料行，可能會影響應用程式
  trigger_schemaias sp_helptrigger 系統預存程式所傳回之結果集中的最後一個資料行。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 若要取得針對特定資料表定義之觸發程序的相關資訊，請查詢 sys.triggers 目錄檢視。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>更正動作  
 請檢閱 sp_helptrigger 在應用程式中的使用方式。 您可能需要修改應用程式，以配合其他資料行。 或者，您也可以改用 sys.triggers 目錄檢視。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫引擎升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor &#91;新的&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
