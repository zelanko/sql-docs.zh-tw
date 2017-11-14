---
title: "保護 RDS 應用程式 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RDS security [ADO]
ms.assetid: 82fb1330-d6c6-4c17-ad3e-d417ff822b25
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 72a46915beed5bb65953788b2b1b7283d90cb8e5
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="securing-rds-applications"></a>保護 RDS 應用程式
本主題提供.rds 的安全性資訊  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件已不再包含在 Windows 作業系統中 (請參閱 < Windows 8 和[Windows Server 2012 相容性手冊](https://www.microsoft.com/en-us/download/details.aspx?id=27416)如需詳細資訊)。 Windows 的未來版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉到[WCF 資料服務](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="microsoft-internet-explorer-security-issues"></a>Microsoft Internet Explorer 安全性問題  
 與 Microsoft Internet explorer 中加入新的安全性增強功能，某些 ADO 和 RDS 物件的限制為僅在 「 安全 」 的模式環境下執行。 這需要您了解這些問題，包括不同的區域、 安全性層級、 嚴格的行為、 不安全的作業和自訂安全性設定。  
  
## <a name="security-and-your-web-server"></a>安全性和網頁伺服器  
 如果您使用[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)網際網路網頁伺服器上的物件，請記住，這麼做，會建立潛在的安全性風險。 取得有效的資料來源名稱 (DSN)、 使用者識別碼和密碼資訊的外部使用者無法撰寫網頁傳送到該資料來源的任何查詢。 如果您想要限制的存取資料來源，其中一個選項是要取消登錄並刪除**RDSServer.DataFactory**物件 (msadcf.dll)，並改為使用硬式編碼查詢中使用自訂的商務物件。  
  
 如需有關使用 RDSServer.DataFactory 物件的安全性含意的詳細資訊，請參閱 Microsoft 安全性網站上的 Microsoft 安全性公告 MS99 025 視窗。  
  
## <a name="client-impersonation-and-security"></a>用戶端模擬和安全性  
 如果**密碼驗證**IIS Web 伺服器 屬性設定為 Windows NT 挑戰/回應驗證 （適用於 Windows NT 4.0) 或 （適用於 Windows 2000) 的整合式 Windows 驗證，則商務物件用戶端的安全性內容下叫用。 這是允許透過 HTTP 的用戶端模擬的 RDS 1.5 的新功能。 在此模式中工作時，網頁伺服器 (IIS) 來登入不是匿名的但使用的使用者識別碼和用戶端電腦正在執行的密碼。 如果 ODBC Dsn 會設定為使用信任連接，然後存取資料庫，例如 SQL Server，也不會在用戶端的安全性內容下。 但這只適用於資料庫是否位於與 IIS; 相同的電腦上用戶端的認證無法轉至尚未另一部電腦。  
  
 例如，用戶端中，John Doe userid ="JohnD"和密碼 = 「 密碼 」 登入用戶端電腦。 他會執行需要存取的瀏覽器型應用程式**RDSServer.DataFactory**物件以建立[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)"MyServer"電腦上執行 SQL 查詢來執行 IIS。 MyServer，執行 Windows NT Server 4.0 的系統設定為使用 Windows NT 挑戰/回應驗證、 其 ODBC DSN 中具有使用信任連接 」 選取，而且伺服器也包含 SQL Server 資料來源。 在 Web 伺服器上收到要求時，它會要求用戶端的使用者識別碼和密碼。 因此，要求以登入 MyServer 來自 「 JohnD 」 / 「 密碼 」 而不是 IUSER_MyServer （即預設匿名密碼驗證時）。 同樣地，登入 SQL Server，"JohnD"時使用 「 密碼 」。  
  
 因此，IIS Windows NT 挑戰/回應驗證模式允許未明確的登入資料庫所需的使用者識別碼和密碼資訊提示使用者建立的 HTML 頁面。 如果使用 IIS 基本驗證時，則這也是必要。  
  
## <a name="password-authentication"></a>密碼驗證  
 RDS 可以與任何一種三種密碼驗證模式執行的 IIS Web 伺服器進行通訊： 匿名、 基本、 或 NT Challenge/Response 驗證 （Windows 2000 中稱為整合式 Windows 驗證）。 這些設定會定義如何將 Web 伺服器控制項存取透過它，例如要求用戶端電腦在 NT Web 伺服器上有明確的存取權限。



