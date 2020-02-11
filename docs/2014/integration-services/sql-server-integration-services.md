---
title: SQL Server Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS
- DTS [Integration Services]
- SQL Server Integration Services
- Integration Services
- DTS [Integration Services], about Integration Services
- data integration [Integration Services]
- Data Transformation Services
ms.assetid: c4398655-5657-4ae4-a690-a380790fe84f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 046058aa9c00cafb9a5ab9aac61b14d1d78668fc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62766474"
---
# <a name="sql-server-integration-services"></a>SQL Server Integration Services
  
[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]是用來建立企業級資料整合和資料轉換方案的平臺。 您可利用下列方式使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 解決複雜的商務問題：複製或下載檔案、傳送電子郵件訊息以回應事件、更新資料倉儲、清理和採礦資料，以及管理 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 物件和資料。 這些封裝可單獨使用或搭配其他封裝使用，以因應複雜的商務需求。 
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 可從各種來源 (如 XML 資料檔案、一般檔案與關聯式資料來源) 擷取與轉換資料，然後再將該資料載入一個或多個目的地。<br /><br /> 
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包含一組豐富的內建工作和轉換；建構封裝的工具；以及執行和管理封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務。 您可使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 圖形工具建立方案，而不需要撰寫任何程式碼；或者，您也可以撰寫擴充 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 物件模型，以程式設計方式建立封裝及撰寫自訂工作和其他封裝物件。<br /><br /> **依區域流覽內容**<br /> ![小型檔案資料夾圖示](media/filefolder-small.gif "小型檔案資料夾圖示")[新功能](what-s-new-in-integration-services-in-sql-server-2016.md)<br /><br /> ![小型檔案資料夾圖示](media/filefolder-small.gif "小型檔案資料夾圖示")回溯[相容性](integration-services-backward-compatibility.md)<br /><br /> ![小型檔案資料夾圖示](media/filefolder-small.gif "小型檔案資料夾圖示") [Integration Services 功能和](../../2014/integration-services/integration-services-features-and-tasks.md)工作<br /><br /> ![小型檔案資料夾圖示](media/filefolder-small.gif "小型檔案資料夾圖示")[技術參考](../../2014/integration-services/technical-reference-integration-services.md)  
  
 [公司資訊管理（EIM）：將 SSIS、DQS 和 MDS 結合](https://go.microsoft.com/fwlink/?LinkId=258672)在 channel9.msdn.com 上。  
  
![Integration Services 圖示（小型）](media/dts-16.gif "Integration Services 圖示 (小)")**與 Integration Services 保持最**新狀態  <br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
  
