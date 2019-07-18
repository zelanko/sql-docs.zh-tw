---
title: 嘗試建立連線時發生錯誤 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 28d5bd077da96e3dd6f8a48004c3a5df1b681f61
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208350"
---
# <a name="an-error-occurred-during-an-attempt-to-establish-a-connection"></a>嘗試建立連線時發生錯誤
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  如果您在沒有安裝 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 的伺服器上查詢 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料，就會發生此錯誤。 它也會發生 如果 SQL Server Analysis Services ( [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) 服務已停止，或如果您嘗試檢視[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]從較早版本的資料。  
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|適用對象|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint|  
|產品版本|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|資料連接失敗。|  
|訊息文字|嘗試建立與外部資料來源之間的連接時，發生錯誤。 下列連接無法重新整理：[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料|  
  
## <a name="explanation"></a>說明  
 Excel Services 會傳回此錯誤，當您查詢[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]Excel 活頁簿發行至 SharePoint，而 SharePoint 環境中的資料沒有[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]for SharePoint 伺服器或 SQL Server Analysis Services ( [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)])服務已停止。  
  
 如果查詢引擎無法使用，您在配量或篩選 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料時將會發生這個錯誤。  
  
## <a name="user-action"></a>使用者動作  
 安裝 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 或是將 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿移到已安裝 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 的 SharePoint 環境。 如需詳細資訊，請參閱 [Power Pivot for SharePoint 2010 安裝](http://msdn.microsoft.com/8d47dde7-c941-4280-a934-e2fe3f9a938f)。  
  
 如果已安裝軟體，請確認 SQL Server Analysis Services ( [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) 執行個體正在執行。 核取 [管理中心] 內的 [管理伺服器上的服務]  。 此外，請檢查 [系統管理工具] 中的 [服務] 主控台應用程式。  
  
 若是在 SQL Server 2008 R2 版 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel 中建立的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿，您必須安裝 SQL Server 2008 R2 版的 Analysis Services OLE DB 提供者。 如果安裝了此提供者，但沒有註冊 Microsoft.AnalysisServices.ChannelTransport.dll 檔案，就會發生此錯誤。 如需檔案註冊的詳細資訊，請參閱[在 SharePoint 伺服器上安裝 Analysis Services OLE DB 提供者](http://msdn.microsoft.com/2c62daf9-1f2d-4508-a497-af62360ee859)。  
  
## <a name="see-also"></a>另請參閱  
 [資料連接使用 Windows 驗證，而無法委派使用者認證。下列連接無法重新整理：Power Pivot 資料](../../analysis-services/power-pivot-sharepoint/the-data-connection-user-could-not-be-delegated.md)  
  
  
