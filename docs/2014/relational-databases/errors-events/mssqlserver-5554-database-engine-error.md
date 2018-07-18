---
title: MSSQLSERVER_5554 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 5554 (Database Engine error)
ms.assetid: 7134bbe5-d240-4a98-85ce-b13cc8ae9b0e
caps.latest.revision: 11
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1c7db414ef084b8117b93607e13d76ec128688db
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37423867"
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
  
  
