---
description: 為安全或不受限制模式設定 DataFactory
title: 為安全或不受限制的模式設定 DataFactory |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory configuration in RDS [ADO]
ms.assetid: 8ff24805-dc7a-42ae-b600-5bad0e3f51b8
author: rothja
ms.author: jroth
ms.openlocfilehash: ab1236205813d1fa3aee0a039703afb10661169c
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978359"
---
# <a name="configuring-datafactory-for-safe-or-unrestricted-modes"></a>為安全或不受限制模式設定 DataFactory
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 根據預設，ADO 會安裝「安全」的 [RDSServer DataFactory](../../reference/rds-api/datafactory-object-rdsserver.md) 設定。 RDS 伺服器元件的安全模式表示下列情況成立：  
  
1.  RDSServer. DataFactory 需要處理常式 (這是由登錄機碼設定) 所強制。  
  
2.  預設處理常式 msdfmap 會註冊、出現在安全處理常式清單中，並標示為預設處理常式。  
  
3.  Msdfmap.ini 檔案安裝在 Windows 目錄中。 您必須根據自己的需求來設定此檔案，才能在三層模式中使用 RDS。  
  
 （選擇性）您可以設定不受限制的 **DataFactory** 安裝。 您可以直接使用**DataFactory** ，而不需要使用自訂處理常式。 使用者仍然可以藉由修改連接字串來使用自訂處理常式，但這不是必要的。 如需有關使用 **RDSServer DataFactory** 物件之含意的詳細資訊，請參閱 [保護 RDS 應用程式](./securing-rds-applications.md)。  
  
 已提供登錄檔 handsafe 來設定安全設定的處理常式登錄專案。 若要在安全模式中執行，請執行 handsafe .reg。  
  
 執行 handsafe 之後，您必須在 [命令提示字元] 視窗中輸入下列命令，以停止並重新啟動 Web 服務器上的 World Wide Web 發行服務： "NET STOP W3SVC" 和 "NET START W3SVC"。  
  
## <a name="see-also"></a>另請參閱  
 [DataFactory 自訂](./datafactory-customization.md)   
 [RDS 基本概念](./rds-fundamentals.md)