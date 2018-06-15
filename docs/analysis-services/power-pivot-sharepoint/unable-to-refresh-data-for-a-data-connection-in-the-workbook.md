---
title: 無法重新整理活頁簿中的資料連接 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d1fabd45d3b9858114e48e3bdde258ed6ccc8362
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34037422"
---
# <a name="unable-to-refresh-data-for-a-data-connection-in-the-workbook"></a>無法重新整理活頁簿中資料連接的資料
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  如果是包含 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料的 Excel 活頁簿，Excel Services 會在提交連接要求至 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 伺服器而且該要求失敗時，傳回這個錯誤。  
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|適用於：|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 安裝|  
|제품 버전|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|請參閱下列內容。|  
|메시지 텍스트|無法重新整理活頁簿中資料連接的資料。 請再試一次或連絡系統管理員。 下列連接無法重新整理︰ [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料|  
  
## <a name="explanation-and-resolution"></a>說明與解決方法  
 Excel Services 無法連接或載入 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料。 發生此錯誤的條件包括：  
  
 **案例 1：未啟動服務**  
  
 未啟動 SQL Server Analysis Services ([!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) 執行個體。 過期的密碼使伺服器停止執行。 如需有關變更密碼的詳細資訊，請參閱＜ [設定 Power Pivot 服務帳戶](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md) ＞和＜ [啟動或停止 Power Pivot for SharePoint Server](../../analysis-services/power-pivot-sharepoint/start-or-stop-a-power-pivot-for-sharepoint-server.md)＞。  
  
 **案例 2a：在伺服器上開啟舊版活頁簿**  
  
 您嘗試開啟的活頁簿可能已在 SQL Server 2008 R2 版的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel 中建立。 最有可能是因為資料連接字串中指定的 Analysis Services 資料提供者不存在於處理要求的電腦上。  
  
 如果這種情況，您會發現此訊息在 ULS 記錄檔中: 「 重新整理失敗 '[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]t Data' 活頁簿中'\<活頁簿 URL >'"，後面接著 「 無法取得連接 」。  
  
 若要判斷活頁簿的版本，您可以在 Excel 開啟它並檢查連接字串中指定的資料提供者。 SQL Server 2008 R2 活頁簿使用 MSOLAP.4 做為其資料提供者。  
  
 若要解決此問題，您可以升級活頁簿。 或者，您也可以在執行 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 或 Excel Services 的實體電腦上安裝 SQL Server 2008 R2 版 Analysis Services 的用戶端程式庫， [在 SharePoint 伺服器上安裝 Analysis Services OLE DB 提供者](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859)。  
  
 **案例 2b：在用戶端程式庫版本錯誤的應用程式伺服器上執行 Excel Services**  
  
 根據預設，SharePoint Server 2010 會在執行 Excel Services 的應用程式伺服器上安裝 SQL Server 2008 版的 Analysis Services OLE DB 提供者。 在支援 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料存取的伺服器陣列中，執行要求 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料之應用程式 (例如 Excel Services 和 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint) 的所有實體伺服器上都必須使用更新版本的資料提供者。  
  
 執行 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 的伺服器會自動取得更新的 OLE DB 資料提供者。 其他伺服器，例如執行 Excel Services 獨立執行個體但在相同電腦上並沒有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 的伺服器，則必須先安裝修補程式，以使用較新版的用戶端程式庫。 如需詳細資訊，請參閱 [Install the Analysis Services OLE DB Provider on SharePoint Servers](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859)。  
  
 **案例 3：網域控制站無法使用**  
  
 可能是無法使用網域控制站驗證使用者識別所致。 對 Windows Token Service 的宣告需要網域控制站，才能針對每個連接驗證 SharePoint 使用者。 對 Windows Token Service 的宣告無法使用快取認證。 它會針對每一個連接來驗證使用者識別。  
  
 您可以檢視 SharePoint 記錄檔來確認這個錯誤的原因。 如果 SharePoint 記錄檔包含「無法從 IClaimsIdentity 取得 WindowsIdentity」訊息，則表示無法驗證使用者識別。  
  
 若要解決此問題，請將電腦加入至與 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 伺服器相同的網域，或在本機電腦上安裝網域控制站。 第二個解決方案「安裝網域控制站」將需要您為所有服務和使用者建立本機網域帳戶。 您將需要為您定義的帳戶設定服務帳戶和 SharePoint 權限。  
  
 如果您的目標是在離線狀態下使用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint，在電腦上安裝網域控制站相當實用。 如需有關如何使用的詳細指示[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]離線，請參閱部落格文章，以"採取您[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]離線的伺服器 」 上[ http://www.powerpivotgeek.com ](http://go.microsoft.com/fwlink/?LinkId=184241)。  
  
 **案例 4：伺服器不穩定**  
  
 可能有一項或多項服務處於不一致的狀態。 在某些情況下，執行 IISRESET 即可解決問題。  
  
  
