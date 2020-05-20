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
author: rothja
ms.author: jroth
ms.openlocfilehash: f785eed6124970d8c270492b98dc8e5ea815f18a
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758964"
---
# <a name="securing-rds-applications"></a>保護 RDS 應用程式
本主題提供 RDS 的安全性資訊。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統不再包含 RDS 伺服器元件（如需詳細資訊，請參閱 Windows 8 和[Windows Server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416)）。 RDS 用戶端元件將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至[WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="microsoft-internet-explorer-security-issues"></a>Microsoft Internet Explorer 安全性問題  
 Microsoft Internet Explorer 加入了新的安全性增強功能，部分 ADO 和 RDS 物件僅限於在「安全」模式環境中執行。 這需要您瞭解這些問題，包括不同的區域、安全性等級、限制的行為、unsafe 作業，以及自訂的安全性設定。  
  
## <a name="security-and-your-web-server"></a>安全性和您的網頁伺服器  
 如果您在網際網路 Web 服務器上使用[RDSServer. DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)物件，請記住，這麼做會造成潛在的安全性風險。 取得有效資料來源名稱（DSN）、使用者識別碼和密碼資訊的外部使用者可以撰寫頁面，將任何查詢傳送至該資料來源。 如果您想要更受限制地存取資料來源，其中一個選項是取消註冊並刪除**RDSServer. DataFactory**物件（msadcf），並改為使用自訂商務物件與硬式編碼的查詢。  
  
 如需有關使用 RDSServer. DataFactory 物件之安全性含意的詳細資訊，請參閱 Microsoft 安全性網站上的 Microsoft 資訊安全公告 MS99-025。  
  
## <a name="client-impersonation-and-security"></a>用戶端模擬和安全性  
 如果 IIS Web 服務器的 [**密碼驗證**] 內容設定為 [Windows nt 挑戰/回應驗證] （適用于 windows nt 4.0）或整合式 windows 驗證（適用于 windows 2000），則會在用戶端的安全性內容下叫用商務物件。 這是 RDS 1.5 中的新功能，可允許透過 HTTP 進行用戶端模擬。 在此模式下工作時，登入網頁伺服器（IIS）不是匿名的，而是使用執行用戶端電腦的使用者識別碼和密碼。 如果 ODBC Dsn 設定為使用信任連接，則存取資料庫（例如 SQL Server）也會在用戶端的安全性內容下發生。 但這只有在資料庫與 IIS 位於相同的電腦上時才適用;用戶端認證無法執行至另一部電腦。  
  
 例如，具有 userid = "JohnD" 且 password = "secret" 的用戶端 John Doe 已登入用戶端電腦。 他執行的瀏覽器應用程式需要存取**RDSServer. DataFactory**物件，藉由在執行 IIS 的 "MyServer" 電腦上執行 SQL 查詢來建立[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。 MyServer，執行 Windows NT Server 4.0 的系統設定為使用 Windows NT 挑戰/回應驗證，其 ODBC DSN 已選取 [使用信任的連線]，而伺服器也包含 SQL Server 的資料來源。 在 Web 服務器上收到要求時，會要求用戶端提供使用者識別碼和密碼。 因此，此要求會在 MyServer 上記錄為來自 "JohnD"/"Secret"，而不是 IUSER_MyServer （這是匿名密碼驗證開啟時的預設值）。 同樣地，登入 SQL Server 時，會使用 "JohnD"/"Secret"。  
  
 因此，IIS Windows NT 挑戰/回應驗證模式可讓您建立 HTML 網頁，而不會明確提示使用者輸入登入資料庫所需的使用者識別碼和密碼資訊。 如果使用 IIS 基本驗證，這也是必要的。  
  
## <a name="password-authentication"></a>密碼驗證  
 RDS 可以與下列三種密碼驗證模式中的任何一個執行的 IIS Web 服務器通訊：匿名、基本或 NT 挑戰/回應驗證（在 Windows 2000 中稱為整合式 Windows 驗證）。 這些設定會定義 Web 服務器如何透過它來控制存取，例如要求用戶端電腦在 NT Web 服務器上擁有明確的存取權限。


