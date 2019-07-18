---
title: MSSQLSERVER_5554 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 5554 (Database Engine error)
ms.assetid: 7134bbe5-d240-4a98-85ce-b13cc8ae9b0e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c3b8e4690b0e0c501fee26648cd9632fdcf28b1d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62913684"
---
# <a name="mssqlserver5554"></a>MSSQLSERVER_5554
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|MSSQLSERVER|  
|事件識別碼|5554|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|FS_MINIVER_OVERFLOW|  
|訊息文字|單一檔案的版本總數已到達檔案系統設定的上限。|  
  
## <a name="explanation"></a>說明  
 在 Multiple Active Result Sets (MARS) 或觸發程序案例中，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用作業系統所指定的迷你版本。  
  
## <a name="user-action"></a>使用者動作  
 嘗試避免重複更新相同交易內的資料。  
  
  
