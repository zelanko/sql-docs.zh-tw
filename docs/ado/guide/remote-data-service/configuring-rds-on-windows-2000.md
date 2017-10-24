---
title: "在 Windows 2000 上設定 RDS |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RDS configuration [ADO], Windows 2000
ms.assetid: ef37e858-c05f-4f52-a65f-3ce6037e0d03
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cf283b40d32f26b916d87ecf7d6946bf97eea415
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="configuring-rds-on-windows-2000"></a>在 Windows 2000 設定的 RDS
如果您遇到取得 RDS 升級為 Windows 2000 之後正常運作的問題，請遵循下列步驟來疑難排解此問題：  
  
1.  請確定使用 Internet Explorer 瀏覽至 http:// 伺服器執行第一個 World Wide Web Publishing 服務。 如果您無法存取 Web 伺服器，以這種方式，開啟命令提示字元，並輸入下列命令，也就是"NET 啟動 W3SVC"。  
  
2.  在 [開始] 功能表上選取 [執行]。 輸入 msdfmap.ini，然後按一下 [確定] 以開啟 [記事本] 中的 msdfmap.ini 檔案。 檢查 [預設連線] 區段中，並存取參數設定為 NOACCESS，如果將它變更為唯讀。  
  
3.  使用 [RegEdit] 公用程式，瀏覽至"HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DataFactory\HandlerInfo 」，並確定**HandlerRequired**設為 0 和**DefaultHandler**是""(Null 字串)。  
  
     **請注意**如果您要登錄此區段進行任何變更，您必須停止並重新啟動 World Wide Web Publishing 服務，輸入下列命令，在命令提示字元:"NET 停止 W3SVC"和"NET 啟動 W3SVC"。  
  
4.  使用 RegEdit 公用程式，瀏覽 」 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W3SVC\Parameters\ADCLaunch"登錄中，確認沒有名為**RDSServer.Datafactory**。 否則，請建立它。  
  
5.  使用網際網路服務管理員，找出預設的網站，並檢視 MSADC 虛擬根目錄的屬性。 檢查 目錄安全性/IP 位址和網域名稱限制。 如果已核取 「 存取被拒 」，然後選取"Granted"。  
  
 嘗試重新啟動伺服器，如果確定不會出現以解決此問題，一開始的變更。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件都不再隨附於 Windows 作業系統。 使用以 RDS 的應用程式移轉[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="see-also"></a>另請參閱  
 [RDS 基本概念](../../../ado/guide/remote-data-service/rds-fundamentals.md)



