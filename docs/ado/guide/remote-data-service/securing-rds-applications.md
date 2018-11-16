---
title: 保護 RDS 應用程式 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS security [ADO]
ms.assetid: 82fb1330-d6c6-4c17-ad3e-d417ff822b25
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d41a1150a2562779f233454ae32949310cde600e
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/12/2018
ms.locfileid: "51559975"
---
# <a name="securing-rds-applications"></a>保護 RDS 應用程式
本主題提供 RDS 的安全性資訊  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，RDS 伺服器元件不會再包含在 Windows 作業系統中 (請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)如需詳細資訊)。 RDS 用戶端元件將會在 Windows 的未來版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該移轉至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="microsoft-internet-explorer-security-issues"></a>Microsoft Internet Explorer 的安全性問題  
 透過新加入 Microsoft Internet Explorer 的安全性增強功能，某些 ADO 和 RDS 物件的限制為只在 「 安全 」 的模式環境下執行。 這需要您注意這些問題，包括不同的區域、 安全性層級、 嚴格的行為、 不安全的作業，並自訂安全性設定。  
  
## <a name="security-and-your-web-server"></a>安全性和網頁伺服器  
 如果您使用[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)網際網路網頁伺服器上的物件，請記住，這麼做會有潛在的安全性風險。 取得有效的資料來源名稱 (DSN)、 使用者識別碼和密碼資訊的外部使用者可以撰寫任何查詢傳送到該資料來源的頁面。 如果您想要更具限制性的存取資料來源，其中一個選項是取消註冊，並刪除**RDSServer.DataFactory**物件 (msadcf.dll)，並改為使用硬式編碼查詢中使用自訂商務物件。  
  
 如需有關使用 RDSServer.DataFactory 物件的安全性含意的詳細資訊，請參閱 Microsoft 安全性網站上的 Microsoft 安全性公告 MS99 025 視窗。  
  
## <a name="client-impersonation-and-security"></a>用戶端模擬和安全性  
 如果**密碼驗證**IIS 網頁伺服器 屬性設定 （適用於 Windows NT 4.0) 的 Windows NT Challenge/Response 驗證或整合式 Windows 驗證 （適用於 Windows 2000)，則商務物件叫用用戶端的安全性內容下。 這是允許透過 HTTP 的用戶端模擬的 RDS 1.5 的新功能。 在此模式中時，網頁伺服器 (IIS) 來登入不是匿名的但使用的使用者識別碼和用戶端電腦執行的密碼。 如果 ODBC Dsn 會設定為使用信任連接，然後存取資料庫，例如 SQL Server，也會在用戶端的安全性內容下。 但這只適用於資料庫是否位於與 IIS; 在同一部電腦上用戶端認證均不得結轉到另一個的電腦。  
  
 例如，用戶端中，John Doe，userid ="JohnD"和密碼 = 「 密碼 」 登入的用戶端電腦。 他會執行的瀏覽器為基礎的應用程式需要存取**RDSServer.DataFactory**物件來建立[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)"MyServer"電腦上執行 SQL 查詢來執行 IIS。 MyServer，執行 Windows NT Server 4.0 的系統設定為使用 Windows NT Challenge/Response 驗證，及其 ODBC DSN [使用信任連線] 選取，而且伺服器也包含 SQL Server 資料來源。 在 Web 伺服器收到要求時，它會要求用戶端的使用者識別碼和密碼。 因此，要求以登入 MyServer 來自"JohnD 」 / 「 密碼 」 而不是 IUSER_MyServer （這是預設值，匿名密碼驗證時）。 同樣地，登入 SQL Server 中，「 JohnD"時使用 「 密碼 」。  
  
 因此，IIS Windows NT Challenge/Response 驗證模式允許建立，而不會明確提示使用者登入資料庫所需的使用者識別碼和密碼資訊的 HTML 頁面。 如果已使用 IIS 基本驗證，則這也會需要。  
  
## <a name="password-authentication"></a>密碼驗證  
 RDS 可與執行中的三種密碼驗證模式的任何一個 IIS Web 伺服器通訊： 匿名、 基本、 或 NT Challenge/Response 驗證 （Windows 2000 中稱為整合式 Windows 驗證）。 這些設定會定義如何在 Web 伺服器控制透過它，例如要求的用戶端電腦擁有明確的存取權限，NT Web 伺服器上的存取權。


