---
title: 無法重新整理活頁簿中資料連接的資料。 請再試一次或連絡系統管理員。 下列連接無法重新整理： PowerPivot 資料 |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0f6fd52d-ac72-43e3-aa08-05a2d2bb873d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 81e99fc17cb8f369967ff4c26699e67f0ed91d33
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66070937"
---
# <a name="unable-to-refresh-data-for-a-data-connection-in-the-workbook-try-again-or-contact-your-system-administrator-the-following-connections-failed-to-refresh-powerpivot-data"></a>無法重新整理活頁簿中資料連接的資料。 請再試一次或連絡系統管理員。 下列連接無法重新整理：PowerPivot 資料
  如果是包含 PowerPivot 資料的 Excel 活頁簿，Excel Services 會在提交連接要求至 PowerPivot 伺服器而且該要求失敗時，傳回這個錯誤。  
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|適用於：|PowerPivot for SharePoint 安裝|  
|產品版本|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|請參閱下列內容。|  
|訊息文字|無法重新整理活頁簿中資料連接的資料。 請再試一次或連絡系統管理員。 下列連接無法重新整理：PowerPivot 資料|  
  
## <a name="explanation-and-resolution"></a>說明與解決方法  
 Excel Services 無法連接或載入 PowerPivot 資料。 發生此錯誤的條件包括：  
  
 **案例 1：未啟動服務**  
  
 未啟動 SQL Server Analysis Services (PowerPivot) 執行個體。 過期的密碼使伺服器停止執行。 如需變更密碼的詳細資訊，請參閱[設定 PowerPivot 服務帳戶](configure-power-pivot-service-accounts.md)和[啟動或停止 PowerPivot for SharePoint 伺服器](start-or-stop-a-power-pivot-for-sharepoint-server.md)。  
  
 **案例 2a：在伺服器上開啟舊版活頁簿**  
  
 您嘗試開啟的活頁簿可能是在 SQL Server 2008 R2 版的 PowerPivot for Excel 中建立。 最有可能是因為資料連接字串中指定的 Analysis Services 資料提供者不存在於處理要求的電腦上。  
  
 如果是這種情況，您會在 ULS 記錄檔中發現此訊息：「活頁簿的\<URL 中的 ' PowerPivot 資料 ' 重新整理失敗> '」，後面接著「無法取得連接」。  
  
 若要判斷活頁簿的版本，您可以在 Excel 開啟它並檢查連接字串中指定的資料提供者。 SQL Server 2008 R2 活頁簿使用 MSOLAP.4 做為其資料提供者。  
  
 若要解決此問題，您可以升級活頁簿。 或者，您也可以在執行 PowerPivot for SharePoint 或 Excel Services 的實體電腦上安裝 SQL Server 2008 R2 版 Analysis Services 的用戶端程式庫。  
  
 [在 SharePoint 伺服器上安裝 Analysis Services OLE DB 提供者](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)  
  
 **案例 2b：在用戶端程式庫版本錯誤的應用程式伺服器上執行 Excel Services**  
  
 根據預設，SharePoint Server 2010 會在執行 Excel Services 的應用程式伺服器上安裝 SQL Server 2008 版的 Analysis Services OLE DB 提供者。 在支援 PowerPivot 資料存取的伺服器陣列中，執行要求 PowerPivot 資料之應用程式 (例如 Excel Services 和 PowerPivot for SharePoint) 的所有實體電腦上都必須使用更新版本的資料提供者。  
  
 執行 PowerPivot for SharePoint 的伺服器會自動取得更新的 OLE DB 資料提供者。 其他伺服器，例如執行 Excel Services 獨立執行個體但在相同電腦上並沒有 PowerPivot for SharePoint 的應用程式伺服器，則必須先安裝修補程式，以使用較新版的用戶端程式庫。 如需詳細資訊，請參閱 [在 SharePoint 伺服器上安裝 Analysis Services OLE DB 提供者](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)。  
  
 **案例 3：網域控制站無法使用**  
  
 可能是無法使用網域控制站驗證使用者識別所致。 對 Windows Token Service 的宣告需要網域控制站，才能針對每個連接驗證 SharePoint 使用者。 對 Windows Token Service 的宣告無法使用快取認證。 它會針對每一個連接來驗證使用者識別。  
  
 您可以檢視 SharePoint 記錄檔來確認這個錯誤的原因。 如果 SharePoint 記錄檔包含「無法從 IClaimsIdentity 取得 WindowsIdentity」訊息，則表示無法驗證使用者識別。  
  
 若要解決此問題，請將電腦加入至與 PowerPivot 伺服器相同的網域，或在本機電腦上安裝網域控制站。 第二個解決方案「安裝網域控制站」將需要您為所有服務和使用者建立本機網域帳戶。 您將需要為您定義的帳戶設定服務帳戶和 SharePoint 權限。  
  
 如果您的目標是在離線狀態下使用 PowerPivot for SharePoint，在電腦上安裝網域控制站相當實用。 如需有關如何離線使用 PowerPivot 的詳細指示，請參閱的「在網路上[http://www.powerpivotgeek.com](https://go.microsoft.com/fwlink/?LinkId=184241)取得您的 PowerPivot 服務器」的 blog 專案。  
  
 **案例 4：伺服器不穩定**  
  
 可能有一項或多項服務處於不一致的狀態。 在某些情況下，執行 IISRESET 即可解決問題。  
  
  
