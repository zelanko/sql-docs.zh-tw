---
title: 將來賓許可權授與網頁伺服器電腦 |Microsoft Docs
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
ms.openlocfilehash: bddf6ce0bbfb78435118ef3d87303a94c792c96d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67922641"
---
# <a name="granting-guest-privileges-to-a-web-server-computer"></a>將來賓權限授與網頁伺服器電腦
匿名 Web 服務器帳戶（IUSR_*ComputerName*）必須新增至 Web 服務器電腦上的 [來賓] 本機群組，才能使用 RDS。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
### <a name="to-grant-guest-privileges-to-a-web-server-computer"></a>將來賓許可權授與網頁伺服器電腦  
  
1.  在您的 Microsoft Windows 2000 伺服器電腦上，按一下 [**開始**]，指向 [**程式**]，指向 [系統**管理工具**]，然後按一下 [**電腦管理**]。  
  
2.  在主控台樹的 [**本機使用者和群組**] 中，按一下 [**群組**]。  
  
3.  選取 [**來賓**] 本機群組。 從 [**動作**] 功能表選擇 [**屬性**]。  
  
4.  在 [**來賓屬性**] 對話方塊中，按一下 [**新增**]。  
  
5.  如果匿名 Web 服務器帳戶沒有出現在 [**選取使用者或群組**] 對話方塊的清單中，請將其名稱（IUSR_*ComputerName*）輸入到底部的空白方塊中，然後按一下 [**新增**]。  
  
6.  按一下 [確定]  。


