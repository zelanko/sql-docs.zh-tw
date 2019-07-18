---
title: 修復 Distributed 的 Replay 安裝 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 6fcd8ca8-1ceb-457d-9545-096c74e274d7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ca42f1dda184bf5cd99cad7d34f5ae9fce79478b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66092963"
---
# <a name="repair-a-distributed-replay-installation"></a>修復 Distributed Replay 安裝
  修復 Distributed Replay 元件 (控制器或用戶端) 會執行下列動作：  
  
1.  再次於磁碟上安裝所有相關聯的檔案，並取代任何現有的檔案。  
  
2.  如果已移除對應的服務帳戶，則重新建立 Windows 服務帳戶。  
  
 您無法使用修復作業來加入或移除元件。 新增或移除元件，請選取或取消選取功能樹狀目錄中的對應元件上**特徵**頁面中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝程式。  
  
### <a name="to-repair-a-failed-installation-of-distributed-replay"></a>修復 Distributed Replay 的失敗安裝  
  
1.  從**開始**功能表上，按一下**控制台**，然後按兩下**新增或移除程式**。  
  
2.  選取 [[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中**解除安裝或變更程式**] 視窗中，然後在[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]] 對話方塊中，按一下 [**修復**。  
  
3.  請依照下列中的步驟[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]精靈，然後在**選取功能**頁面上，選取您想要修復，然後按一下 [Distributed Replay 元件**下一步]。** 。  
  
4.  完成 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝精靈，修復選取的 Distributed Replay 功能。  
  
  
