---
title: 在 Windows 2000 上設定 RDS |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS configuration [ADO], Windows 2000
ms.assetid: ef37e858-c05f-4f52-a65f-3ce6037e0d03
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a17ed52371a6c7eae057332a3e80bd215131d287
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704345"
---
# <a name="configuring-rds-on-windows-2000"></a>在 Windows 2000 上設定 RDS
如果您遇到取得 RDS 升級至 Windows 2000 之後正確運作的問題，請遵循下列步驟來排解這個問題：  
  
1.  請確定使用 Internet Explorer 瀏覽至 https:// 伺服器執行第一個 World Wide Web Publishing 服務。 如果您無法存取 Web 伺服器，以這種方式，開啟命令提示字元並輸入下列命令，也就是 「 NET 啟動 W3SVC"。  
  
2.  在 [開始] 功能表上選取 [執行]。 輸入 msdfmap.ini，然後按一下 [確定]，在記事本中開啟 msdfmap.ini 檔案。 檢查 [連線 DEFAULT] 區段中，並存取參數設定為 NOACCESS，如果將它變更為唯讀。  
  
3.  使用 [RegEdit] 公用程式，瀏覽至 「 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DataFactory\HandlerInfo"，並確定**HandlerRequired**設為 0 並**DefaultHandler**是""(Null 字串)。  
  
     **請注意**如果您對登錄的這一部分的任何變更，您必須停止並重新啟動 World Wide Web Publishing 服務，輸入下列命令在命令提示字元："NET STOP W3SVC"和"NET 啟動 W3SVC"。  
  
4.  使用 RegEdit 公用程式，在 「 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W3SVC\Parameters\ADCLaunch"登錄中瀏覽，並確認沒有名為索引鍵**RDSServer.Datafactory**。 否則，請建立它。  
  
5.  使用網際網路服務管理員，找出預設的網站，並檢視 MSADC 虛擬根目錄的屬性。 檢查 目錄安全性/IP 位址和網域名稱限制。 如果已核取 「 拒絕存取 」，然後選取"Granted"。  
  
 請務必嘗試重新啟動伺服器，如果要解決此問題，一開始不會出現變更。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中。 使用 RDS 到應用程式移轉[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="see-also"></a>另請參閱  
 [RDS 基本概念](../../../ado/guide/remote-data-service/rds-fundamentals.md)


