---
title: 將來賓權限授與 Web 伺服器電腦 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- guest privileges in RDS [ADO]
ms.assetid: e851a22d-01bc-4eb0-bc42-92b8f65d1c63
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7fed7d31e0ee52e3f9691913b06f9a9ffede51e7
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704290"
---
# <a name="granting-guest-privileges-to-a-web-server-computer"></a>將來賓權限授與網頁伺服器電腦
匿名的 Web 伺服器帳戶 (iusr_< 電腦*ComputerName*) 必須新增至本機來賓在 Web 伺服器電腦上使用 RDS  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
### <a name="to-grant-guest-privileges-to-a-web-server-computer"></a>若要授與給 Web 伺服器電腦的來賓權限  
  
1.  Microsoft Windows 2000 Server 電腦上，按一下**開始**，指向**程式**，指向**系統管理工具**，然後按一下 **電腦管理**。  
  
2.  在主控台樹狀目錄中，在**本機使用者和群組**，按一下**群組**。  
  
3.  選取 **來賓**本機群組。 從**動作**功能表上，選擇**屬性**。  
  
4.  在 [**來賓屬性**] 對話方塊中，按一下**新增**。  
  
5.  如果匿名的 Web 伺服器帳戶未出現在清單中**選取使用者或群組**對話方塊方塊中輸入其名稱 (iusr_< 電腦*ComputerName*) 到下方的空白方塊，，然後按一下 **新增**.  
  
6.  按一下 [確定]  。


