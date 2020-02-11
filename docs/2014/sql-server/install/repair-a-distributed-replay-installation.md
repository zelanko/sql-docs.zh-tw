---
title: 修復 Distributed Replay 安裝 |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66092963"
---
# <a name="repair-a-distributed-replay-installation"></a>修復 Distributed Replay 安裝
  修復 Distributed Replay 元件 (控制器或用戶端) 會執行下列動作：  
  
1.  再次於磁碟上安裝所有相關聯的檔案，並取代任何現有的檔案。  
  
2.  如果已移除對應的服務帳戶，則重新建立 Windows 服務帳戶。  
  
 您無法使用修復作業來加入或移除元件。 若要新增或移除元件，請在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝程式之 [**特徵選取**] 頁面的功能樹狀結構中，核取或取消核取對應的元件。  
  
### <a name="to-repair-a-failed-installation-of-distributed-replay"></a>修復 Distributed Replay 的失敗安裝  
  
1.  在 [**開始**] 功能表中，按一下 [**控制台**]，然後按兩下 [**新增或移除程式**]。  
  
2.  在[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [**卸載或變更程式**] 視窗中選取，然後在對話方塊[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中按一下 [**修復**]。  
  
3.  依照[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]嚮導中的步驟操作，然後在 [**選取功能**] 頁面上，選取您要修復的 Distributed Replay 元件，然後按 **[下一步]**。  
  
4.  完成 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝精靈，修復選取的 Distributed Replay 功能。  
  
  
