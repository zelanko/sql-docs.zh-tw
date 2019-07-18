---
title: 註冊自訂商務物件 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- custom business object in RDS [ADO]
- registering custom business objects in RDS [ADO]
- business objects in RDS [ADO]
ms.assetid: e9032ad8-d14c-42e3-ba13-cb5f00084a79
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f998463e0f8190aa040b801d2fd29c732bb31dce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922361"
---
# <a name="registering-a-custom-business-object"></a>註冊自訂商務物件
若要成功地透過 Web 伺服器啟動 （.dll 或.exe） 的自訂商務物件，商務物件的 ProgID 必須輸入登錄到此程序中所述。 此 RDS 功能會執行獲批准的可執行檔用來保護您的 Web 伺服器的安全性。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
> [!NOTE]
>  MDAC 2.0 和更新版本的 Windows DAC，預設的商務物件中， [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)，MDAC/Windows DAC 安裝期間未註冊預設情況下。 不過，如果**RDSServer.DataFactory**已註冊為安全的安裝之前的電腦上執行，登錄項目保留在新的安裝。  
  
### <a name="to-register-a-custom-business-object"></a>若要註冊的自訂商務物件：  
  
1.  按一下 **開始**，然後按一下**執行**。  
  
2.  型別**RegEdit**然後按一下**確定**。  
  
3.  在登錄編輯器中，瀏覽至**HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\W3SVC\Parameters\ADCLaunch**登錄機碼。  
  
4.  選取**ADCLaunch**機碼，然後從**編輯**功能表上，指向**新增**然後按一下**金鑰**。  
  
5.  輸入您的自訂商務物件的 ProgID，然後按一下**Enter**。 離開**值**空白的項目。


