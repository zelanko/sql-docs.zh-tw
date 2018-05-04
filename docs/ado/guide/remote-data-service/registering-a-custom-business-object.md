---
title: 註冊自訂的商務物件 |Microsoft 文件
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
- custom business object in RDS [ADO]
- registering custom business objects in RDS [ADO]
- business objects in RDS [ADO]
ms.assetid: e9032ad8-d14c-42e3-ba13-cb5f00084a79
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 025eca1f753c738533298731763fa9c0df70f65e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="registering-a-custom-business-object"></a>註冊自訂的商務物件
若要成功地透過 Web 伺服器啟動自訂的商務物件 （.dll 或.exe），商務物件的 ProgID 必須輸入登錄到此程序中所述。 此 RDS 功能會執行可執行檔保障只能用來保護 Web 伺服器的安全性。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
> [!NOTE]
>  MDAC 2.0 和更新版本和 Windows DAC，預設的商務物件， [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)，MDAC/Windows DAC 安裝期間未註冊預設情況下。 不過，如果**RDSServer.DataFactory**已註冊為安全的安裝之前的電腦上執行，登錄項目會保留新的安裝。  
  
### <a name="to-register-a-custom-business-object"></a>若要註冊自訂的商務物件：  
  
1.  按一下**啟動**，然後按一下 **執行**。  
  
2.  型別**RegEdit**按一下**確定**。  
  
3.  在 登錄編輯器中，瀏覽至**HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\W3SVC\Parameters\ADCLaunch**登錄機碼。  
  
4.  選取**ADCLaunch**索引鍵，然後從**編輯**功能表上，指向**新增**按一下**金鑰**。  
  
5.  輸入您的自訂商務物件的 ProgID，然後按一下**Enter**。 保留**值**空白項目。


