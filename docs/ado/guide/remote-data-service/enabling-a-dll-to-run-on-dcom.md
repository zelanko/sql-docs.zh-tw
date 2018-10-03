---
title: 啟用 DLL 以在 DCOM 上執行 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DLL on DCOM in RDS [ADO]
- DCOM in RDS [ADO]
- business objects in RDS [ADO]
ms.assetid: 5f1c2205-191c-4fb4-9bd9-84c878ea46ed
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 95bfd4d5f5c5dac4f5ee4a74369e68bd40f8f698
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47788846"
---
# <a name="enabling-a-dll-to-run-on-dcom"></a>啟用 DLL 以在 DCOM 上執行
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 下列步驟概述如何啟用使用 DCOM 和 Microsoft 網際網路資訊服務 (HTTP) 透過元件服務的商務物件.dll。  
  
1.  在 [元件服務] MMC 嵌入式管理單元中建立新的空白封裝。  
  
     您將使用 [元件服務] MMC 嵌入式管理單元來建立封裝並加入此封裝的 DLL。 這可讓此.dll 檔可透過 DCOM 存取，但它會移除透過 IIS 存取範圍。 (如果您在登錄中為此.dll 檔中，核取**Inproc**金鑰現在是空的將啟動屬性，在稍後說明本主題中，將值加入中**Inproc**索引鍵。)  
  
2.  安裝封裝中的商務物件。  
  
     -或-  
  
     匯入[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)至封裝的物件。  
  
3.  設定封裝的啟用屬性**在建立者的程序中**（程式庫應用程式）。  
  
     要透過 DCOM 和 IIS 在相同電腦上存取此.dll 檔，您必須在 [元件服務] MMC 嵌入式管理單元中設定元件的啟動屬性。 設定屬性之後**在建立者的程序**，您將會發現**Inproc**已新增登錄機碼伺服器元件服務指向 surrogate.dll。  
  
 如需有關元件服務 （或 Microsoft 交易服務，如果您使用 Windows NT），以及如何執行這些步驟，請造訪 Microsoft 交易 Server 網站。


