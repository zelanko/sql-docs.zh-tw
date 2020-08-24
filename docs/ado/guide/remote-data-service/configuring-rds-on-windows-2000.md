---
description: 在 Windows 2000 上設定 RDS
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 73ab5507d755fed32fa54b36a82f9ca915a8e194
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88758638"
---
# <a name="configuring-rds-on-windows-2000"></a>在 Windows 2000 上設定 RDS
如果您在升級到 Windows 2000 之後遇到 RDS 無法正常運作的問題，請遵循下列步驟來針對問題進行疑難排解：  
  
1.  使用 Internet Explorer 流覽至 HTTPs://伺服器，以確定 World Wide Web 發行服務正在執行。 如果您無法以這種方式存取 Web 服務器，請開啟命令提示字元，並輸入下列命令： "NET START W3SVC"。  
  
2.  在 [[開始] 功能表上，選取 [執行]。 輸入 msdfmap.ini 然後按一下 [確定]，以在 [記事本] 中開啟 msdfmap.ini 檔案。 請檢查 [CONNECT DEFAULT] 區段，如果存取參數設定為 NOACCESS，請將它變更為 READONLY。  
  
3.  使用 RegEdit 公用程式流覽至 "HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\DataFactory\HandlerInfo"，並確定 **HandlerRequired** 設定為0，且 **DefaultHandler** 為 "" (Null 字串) 。  
  
     **注意** 如果您對登錄的這個區段進行任何變更，您必須在命令提示字元中輸入下列命令，以停止並重新啟動 World Wide Web 發行服務：「NET STOP W3SVC」和「NET START W3SVC」。  
  
4.  使用 RegEdit 公用程式，在登錄中流覽至 "HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Services\W3SVC\Parameters\ADCLaunch"，並確認有一個名為 **RDSServer Datafactory**的機碼。 如果沒有，請加以建立。  
  
5.  使用網際網路服務管理員，找出 [預設的網站]，並查看 MSADC 虛擬根目錄的屬性。 檢查目錄的安全性/IP 位址和功能變數名稱限制。 如果已核取 [拒絕存取]，請選取 [已授與]。  
  
 如果一開始就沒有解決問題，請務必嘗試重新開機伺服器。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件。 將使用 RDS 的應用程式遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="see-also"></a>另請參閱  
 [RDS 基本概念](./rds-fundamentals.md)