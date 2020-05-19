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
author: rothja
ms.author: jroth
ms.openlocfilehash: 9f110447fbb0f00c037361b00945b228449caf4f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82747716"
---
# <a name="registering-a-custom-business-object"></a>註冊自訂商務物件
若要透過 Web 服務器成功啟動自訂商務物件（.dll 或 .exe），必須依照此程式中的說明，將商務物件的 ProgID 輸入至登錄中。 此 RDS 功能藉由只執行獲批准可執行檔，來保護 Web 服務器的安全性。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
> [!NOTE]
>  針對 MDAC 2.0 和更新版本和 Windows DAC，預設的商務物件[RDSServer DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)在 MDAC/Windows DAC 安裝期間不會註冊。 不過，如果在安裝之前，已將**RDSServer**註冊為可安全地在電腦上執行，則會針對新的安裝保留登錄專案。  
  
### <a name="to-register-a-custom-business-object"></a>若要註冊自訂商務物件：  
  
1.  按一下 [**開始**]，然後按一下 [**執行**]。  
  
2.  輸入**RegEdit** ，然後按一下 **[確定]**。  
  
3.  在 [登錄編輯程式] 中，流覽至**HKEY_LOCAL_MACHINE \system\currentcontrolset\services\w3svc\parameters\adclaunch**登錄機碼。  
  
4.  選取**ADCLaunch**機碼，然後從 [**編輯**] 功能表指向 [**新增**]，然後按一下 [**金鑰**]。  
  
5.  輸入自訂商務物件的 ProgID，然後按一下**Enter**。 將 [**值**] 專案保留空白。


