---
title: 安全或不受限制的模式設定 DataFactory |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory configuration in RDS [ADO]
ms.assetid: 8ff24805-dc7a-42ae-b600-5bad0e3f51b8
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0ee24eb54db193aa16f15f550de66b92cf9b896c
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66699782"
---
# <a name="configuring-datafactory-for-safe-or-unrestricted-modes"></a>為安全或不受限制模式設定 DataFactory
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 根據預設，使用 「 安全 」 安裝 ADO [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)組態。 RDS 伺服器元件的安全模式，表示在下列條件成立：  
  
1.  處理常式是 RDSServer.DataFactory （這登錄機碼設定所託管） 的必要項目。  
  
2.  預設處理常式、 msdfmap.handler，已登錄，存在於安全處理常式 清單中，並標示為預設處理常式。  
  
3.  Msdfmap.ini 檔案會安裝在 Windows 目錄中。 前三層式模式中使用 RDS，您必須根據您的需求，設定此檔案。  
  
 （選擇性） 您可以設定不受限制**DataFactory**安裝。 **DataFactory**可用的自訂處理常式不直接。 使用者仍然可以藉由修改連接字串中，使用自訂處理常式，但並非必要。 如需有關使用的含意**RDSServer.DataFactory**物件，請參閱[保護 RDS 應用程式](../../../ado/guide/remote-data-service/securing-rds-applications.md)。  
  
 已提供登錄檔案 handsafe.reg 設定安全的組態處理常式登錄項目。 若要在安全模式中執行，執行 handsafe.reg。  
  
 執行 handsafe.reg 之後, 您必須停止並重新啟動 World Wide Web Publishing 服務，在 Web 伺服器上的命令提示字元視窗中輸入下列命令："NET STOP W3SVC"和"NET 啟動 W3SVC"。  
  
## <a name="see-also"></a>另請參閱  
 [DataFactory 自訂](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [RDS 基本概念](../../../ado/guide/remote-data-service/rds-fundamentals.md)



