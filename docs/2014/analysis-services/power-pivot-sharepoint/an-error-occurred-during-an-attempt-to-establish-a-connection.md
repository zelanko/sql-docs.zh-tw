---
title: 嘗試建立與外部資料來源之間的連接時，發生錯誤。 下列連接無法重新整理：PowerPivot Data | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1b951da1-f62d-43d2-b40b-270a4a9ab92c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c09c8984e964b4bdfa93b0fcebae2e613d484892
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66071946"
---
# <a name="an-error-occurred-during-an-attempt-to-establish-a-connection-to-the-external-data-source-the-following-connections-failed-to-refresh-powerpivot-data"></a>嘗試建立與外部資料來源之間的連接時，發生錯誤。 下列連接無法重新整理：PowerPivot 資料
  如果您在沒有安裝 PowerPivot for SharePoint 的伺服器上查詢 PowerPivot 資料，就會發生這個錯誤。 如果 SQL Server Analysis Services (PowerPivot) 服務停止，或者您嘗試從舊版檢視 PowerPivot 資料，也會發生這個錯誤。  
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|適用於|PowerPivot for SharePoint|  
|產品版本|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|原因|資料連接失敗。|  
|訊息文字|嘗試建立與外部資料來源之間的連接時，發生錯誤。 下列連接無法重新整理：PowerPivot 資料|  
  
## <a name="explanation"></a>說明  
 當您查詢發行到 SharePoint 之 Excel 活頁簿中的 PowerPivot 資料，而 SharePoint 環境中沒有 PowerPivot for SharePoint 伺服器或者 SQL Server Analysis Services (PowerPivot) 服務已停止時，Excel Services 即會傳回此錯誤。  
  
 如果查詢引擎無法使用，您在配量或篩選 PowerPivot 資料時將會發生這個錯誤。  
  
## <a name="user-action"></a>使用者動作  
 安裝 PowerPivot for SharePoint 或是將 PowerPivot 活頁簿移到已安裝 PowerPivot for SharePoint 的 SharePoint 環境。 如需詳細資訊，請參閱＜ [PowerPivot for SharePoint 2010 Installation](../../sql-server/install/powerpivot-for-sharepoint-2010-installation.md)＞。  
  
 如果安裝了該軟體，請確認 SQL Server Analysis Services (PowerPivot) 執行個體正在執行。 核取 [管理中心] 內的 [管理伺服器上的服務]  。 此外，請檢查 [系統管理工具] 中的 [服務] 主控台應用程式。  
  
 若是在 SQL Server 2008 R2 版 PowerPivot for Excel 中建立的 PowerPivot 活頁簿，您必須安裝 SQL Server 2008 R2 版的 Analysis Services OLE DB 提供者。 如果安裝了此提供者，但沒有註冊 Microsoft.AnalysisServices.ChannelTransport.dll 檔案，就會發生此錯誤。 如需檔案註冊的詳細資訊，請參閱[在 SharePoint 伺服器上安裝 Analysis Services OLE DB 提供者](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料連接使用 Windows 驗證，而無法委派使用者認證。下列連接無法重新整理：PowerPivot Data](the-data-connection-user-could-not-be-delegated.md)  
  
  
