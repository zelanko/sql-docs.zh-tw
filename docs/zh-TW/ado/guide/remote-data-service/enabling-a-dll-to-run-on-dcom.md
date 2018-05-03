---
title: 啟用在 DCOM 上執行的 DLL |Microsoft 文件
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
- DLL on DCOM in RDS [ADO]
- DCOM in RDS [ADO]
- business objects in RDS [ADO]
ms.assetid: 5f1c2205-191c-4fb4-9bd9-84c878ea46ed
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 79d28f421e5b4c6edcad84ac596c2a109e42f345
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="enabling-a-dll-to-run-on-dcom"></a>啟用在 DCOM 上執行的 DLL
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 下列步驟概述如何啟用使用 DCOM 和 Microsoft 網際網路資訊服務 (HTTP) 透過元件服務的商務物件.dll。  
  
1.  在 [元件服務] MMC 嵌入式管理單元中建立新的空白封裝。  
  
     您將使用 [元件服務] MMC 嵌入式管理單元來建立封裝，並將 DLL 加入至這個封裝。 這樣就可以存取透過 DCOM，此.dll 檔，但它會移除透過 IIS 存取範圍。 (如果您在登錄中為此.dll 檔中，核取**Inproc**金鑰現在是空的將啟動屬性，在稍後說明本主題中，將值加入在**Inproc**索引鍵。)  
  
2.  安裝至封裝中的商務物件。  
  
     -或-  
  
     匯入[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)到封裝物件。  
  
3.  設定封裝的啟動屬性**建立者的程序中**（程式庫應用程式）。  
  
     若要讓此.dll 檔可透過 DCOM 和 IIS 在相同電腦上存取，您必須 [元件服務] MMC 嵌入式管理單元中設定元件的啟動屬性。 將屬性設定為之後**建立者的程序中**，您會注意到**Inproc**已加入伺服器登錄機碼指向元件服務 surrogate.dll。  
  
 如需有關元件服務 （或 Microsoft 交易服務，如果您使用 Windows NT），以及如何執行這些步驟，請瀏覽 Microsoft 交易 Server 網站。


