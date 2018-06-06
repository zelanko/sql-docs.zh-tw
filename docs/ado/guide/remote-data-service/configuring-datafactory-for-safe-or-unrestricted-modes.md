---
title: 為安全 Safe 或不受限制的模式設定 DataFactory |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory configuration in RDS [ADO]
ms.assetid: 8ff24805-dc7a-42ae-b600-5bad0e3f51b8
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e3af0bf538b8d2fb774b06644e8089cf201b5fc6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="configuring-datafactory-for-safe-or-unrestricted-modes"></a>為安全 Safe 或不受限制的模式設定 DataFactory
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 根據預設，ADO 會隨"safe" [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)組態。 安全模式的 RDS 伺服器元件表示在下列條件成立：  
  
1.  處理常式是 RDSServer.DataFactory （這由登錄機碼設定所託管） 的必要項目。  
  
2.  預設處理常式、 msdfmap.handler，已註冊，出現在最安全處理常式清單，並標示為預設處理常式。  
  
3.  Msdfmap.ini 檔案會安裝在 Windows 目錄中。 三層式 」 模式中使用 RDS 之前，您必須根據您的需求，設定此檔案。  
  
 或者，您可以設定不受限制**DataFactory**安裝。 **DataFactory**可以用於直接不使用自訂處理常式。 使用者仍然可以藉由修改連接字串中，使用自訂處理常式，但並非必要。 如需有關使用的含意**RDSServer.DataFactory**物件，請參閱[保護 RDS 應用程式](../../../ado/guide/remote-data-service/securing-rds-applications.md)。  
  
 已提供登錄檔案 handsafe.reg 設定安全組態的處理常式登錄項目。 若要在安全模式中執行，執行 handsafe.reg。  
  
 執行之後 handsafe.reg，您必須停止並重新啟動 World Wide Web Publishing 服務，在 Web 伺服器上，在命令提示字元視窗中輸入下列命令:"NET 停止 W3SVC"和"NET 啟動 W3SVC"。  
  
## <a name="see-also"></a>另請參閱  
 [DataFactory 自訂](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [RDS 基本概念](../../../ado/guide/remote-data-service/rds-fundamentals.md)



