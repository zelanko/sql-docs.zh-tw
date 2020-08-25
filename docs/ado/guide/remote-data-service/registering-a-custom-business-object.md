---
description: 註冊自訂商務物件
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
ms.openlocfilehash: 73b1fe1d0089ed601391f9a621d7cdc163ab8983
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759478"
---
# <a name="registering-a-custom-business-object"></a>註冊自訂商務物件
若要透過 Web 服務器成功啟動自訂的商務物件 ( .dll 或 .exe) ，必須將商務物件的 ProgID 輸入登錄中，如下列程式所述。 此 RDS 功能只會執行獲批准可執行檔，以保護您 Web 服務器的安全性。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
> [!NOTE]
>  針對 MDAC 2.0 和更新版本以及 Windows DAC，預設的商務物件 [RDSServer DataFactory](../../reference/rds-api/datafactory-object-rdsserver.md)在 MDAC/Windows DAC 安裝期間不會依預設註冊。 但是，如果在安裝之前將 **RDSServer** 註冊為安全的電腦上執行，則會保留新安裝的登錄專案。  
  
### <a name="to-register-a-custom-business-object"></a>註冊自訂商務物件：  
  
1.  按一下 [ **開始** ]，然後按一下 [ **執行**]。  
  
2.  輸入 **RegEdit** ，然後按一下 **[確定]**。  
  
3.  在 [登錄編輯程式] 中，流覽至 **HKEY_LOCAL_MACHINE \system\currentcontrolset\services\w3svc\parameters\adclaunch** 登錄機碼。  
  
4.  選取 [ **ADCLaunch** ] 索引鍵，然後從 [ **編輯**] 功能表中指向 [ **新增** ]，然後按一下 [機 **碼**]。  
  
5.  輸入自訂商務物件的 ProgID，然後按一下 **Enter**。 將 [ **值** ] 專案保留空白。