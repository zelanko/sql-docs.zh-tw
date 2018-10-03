---
title: FTP 連接管理員編輯器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.ftpconnectionmanager.f1
helpviewer_keywords:
- FTP Connection Manager Editor
ms.assetid: 874b6585-255b-4a43-8396-bb08c3e8ac2b
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 79f2d2c03d2403042de7f1ca0aeed3db15c93efc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48189138"
---
# <a name="ftp-connection-manager-editor"></a>FTP 連接管理員編輯器
  使用 [FTP 連線管理員編輯器] 對話方塊來指定連接到 FTP 伺服器的屬性。  
  
> [!IMPORTANT]  
>  FTP 連接管理員僅支援匿名驗證和基本驗證， 而不支援 Windows 驗證。  
  
 若要深入了解 FTP 連線管理員，請參閱 [FTP 連線管理員](connection-manager/ftp-connection-manager.md)。  
  
## <a name="options"></a>選項。  
 **伺服器名稱**  
 提供 FTP 伺服器的名稱。  
  
 **伺服器通訊埠**  
 指定 FTP 伺服器上用來連接的通訊埠編號。 這個屬性的預設值為 **21**。  
  
 **使用者名稱**  
 提供存取 FTP 伺服器的使用者名稱。 這個屬性的預設值為 **匿名**。  
  
 **密碼**  
 提供存取 FTP 伺服器的密碼。  
  
 **逾時 (以秒為單位)**  
 指定工作在逾時之前所花的秒數。值為 **0** 指出無限的時間量。 這個屬性的預設值為 **60**。  
  
 **使用被動模式**  
 指定伺服器或用戶端是否起始連接。 伺服器會以主動模式起始連接，而用戶端則會以被動模式啟動連接。 此屬性的預設值為 **主動模式**。  
  
 **重試次數**  
 指定工作嘗試連接的次數。 值為 **0** 指出不限制嘗試次數。  
  
 **區塊大小 (以 KB 為單位)**  
 提供以 KB 為單位的傳輸資料區塊大小。  
  
 **測試連接**  
 設定 FTP 連線管理員之後，請按一下 [測試連接] 以確認連接是可行的。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
