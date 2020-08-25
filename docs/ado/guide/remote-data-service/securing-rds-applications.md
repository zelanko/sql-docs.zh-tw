---
description: 保護 RDS 應用程式
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
ms.openlocfilehash: aff7a1a180e29adf457feab1d0c7f57f4629cfea
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759278"
---
# <a name="securing-rds-applications"></a>保護 RDS 應用程式
本主題提供 RDS 的安全性資訊。  
  
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="microsoft-internet-explorer-security-issues"></a>Microsoft Internet Explorer 安全性問題  
 將新的安全性增強功能新增至 Microsoft Internet Explorer 後，某些 ADO 和 RDS 物件會限制為僅在「安全」模式環境中執行。 這需要您留意這些問題，包括不同的區域、安全性等級、限制行為、不安全的作業，以及自訂的安全性設定。  
  
## <a name="security-and-your-web-server"></a>安全性和您的 Web 服務器  
 如果您在網際網路網頁伺服器上使用 [RDSServer. DataFactory](../../reference/rds-api/datafactory-object-rdsserver.md) 物件，請記住，這麼做會造成潛在的安全性風險。 取得有效資料來源名稱 (DSN) 、使用者識別碼和密碼資訊的外部使用者可以撰寫頁面，將任何查詢傳送到該資料來源。 如果您想要更受限制地存取資料來源，有一個選項是將 **RDSServer. DataFactory** 物件取消註冊並刪除 ( # A0) ，而改為使用自訂商務物件搭配硬式編碼的查詢。  
  
 如需有關使用 RDSServer DataFactory 物件之安全性含意的詳細資訊，請參閱 Microsoft 安全性網站上的 Microsoft 資訊安全公告 MS99-025。  
  
## <a name="client-impersonation-and-security"></a>用戶端模擬和安全性  
 如果您的 IIS Web 服務器的 [ **密碼驗證** ] 屬性設定為 [Windows NT 4.0) Windows NT 挑戰/回應驗證 (，或針對 Windows 2000 Windows 驗證整合 () ，則會在用戶端的安全性內容下叫用商務物件。 這是 RDS 1.5 中的一項新功能，可讓用戶端透過 HTTP 進行模擬。 在此模式下工作時，登入 Web 服務器 (IIS) 不是匿名的，但會使用用戶端電腦執行所在的使用者識別碼和密碼。 如果 ODBC Dsn 設定為使用信任連接，則存取資料庫（例如 SQL Server）也會在用戶端的安全性內容下進行。 但是，這只適用于資料庫位於與 IIS 相同的電腦時;用戶端認證無法轉移到另一部電腦。  
  
 例如，具有 userid = "JohnD" 和 password = "secret" 的用戶端 John Doe 會登入用戶端電腦。 他執行的瀏覽器應用程式需要存取 **RDSServer. DataFactory** 物件，以建立 [記錄集](../../reference/ado-api/recordset-object-ado.md) ，方法是在執行 IIS 的「MyServer」電腦上執行 SQL 查詢。 MyServer 是執行 Windows NT Server 4.0 的系統，設定為使用 Windows NT 挑戰/回應驗證，它的 ODBC DSN 已選取 [使用信任的連線]，而伺服器也包含 SQL Server 資料來源。 當 Web 服務器收到要求時，它會要求用戶端提供使用者識別碼和密碼。 因此，要求會以 MyServer 的形式記錄在 "JohnD"/"Secret"，而不是 IUSER_MyServer (這是在) 上進行匿名密碼驗證時的預設值。 同樣地，當登入 SQL Server 時，會使用 "JohnD"/"Secret"。  
  
 因此，IIS Windows NT 挑戰/回應驗證模式允許建立 HTML 網頁，而不會明確提示使用者登入資料庫所需的使用者識別碼和密碼資訊。 如果正在使用 IIS 基本驗證，則這也是必要的。  
  
## <a name="password-authentication"></a>密碼驗證  
 RDS 可以與在下列三種密碼驗證模式中執行的 IIS Web 服務器通訊：匿名、基本或 NT 挑戰/回應驗證 (在 Windows 2000) 中稱為整合式 Windows 驗證。 這些設定會定義網頁伺服器如何控制其存取，例如要求用戶端電腦必須具有 NT Web 服務器的明確存取權限。