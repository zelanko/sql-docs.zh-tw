---
title: Guest 權限授與 Web 伺服器電腦 |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- guest privileges in RDS [ADO]
ms.assetid: e851a22d-01bc-4eb0-bc42-92b8f65d1c63
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 92d2e20d82f60923381b95e536f3e7ef2b8ae87e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="granting-guest-privileges-to-a-web-server-computer"></a>Guest 權限授與 Web 伺服器電腦
匿名的 Web 伺服器帳戶 (IUSR_<*ComputerName*) 必須新增至本機來賓 Web 伺服器電腦上使用.rds  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
### <a name="to-grant-guest-privileges-to-a-web-server-computer"></a>若要授與 Web 伺服器電腦的 guest 權限  
  
1.  Microsoft Windows 2000 Server 電腦上，按一下 **啟動**，指向 **程式**，指向 **系統管理工具**，然後按一下**電腦管理**。  
  
2.  在主控台樹狀目錄中**本機使用者和群組**，按一下 **群組**。  
  
3.  選取**遊客**本機群組。 從**動作**功能表上，選擇**屬性**。  
  
4.  在**遊客屬性**對話方塊中，按一下 **新增**。  
  
5.  如果匿名的 Web 伺服器帳戶未出現在清單中**選取使用者或群組**對話方塊方塊中輸入其名稱 (IUSR_<*ComputerName*) 到下方空白方塊中，然後再按一下**新增**.  
  
6.  按一下 **[確定]**。


