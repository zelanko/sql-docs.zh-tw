---
title: SQL Server Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SSIS
- DTS [Integration Services]
- SQL Server Integration Services
- Integration Services
- DTS [Integration Services], about Integration Services
- data integration [Integration Services]
- Data Transformation Services
ms.assetid: c4398655-5657-4ae4-a690-a380790fe84f
caps.latest.revision: 47
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 358f11476f8a02037511f55bd2550e817304e80d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023998"
---
# <a name="sql-server-integration-services"></a>SQL Server Integration Services
  
[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 是可建立企業級資料整合和資料轉換方案的平台。 您可利用下列方式使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 解決複雜的商務問題：複製或下載檔案、傳送電子郵件訊息以回應事件、更新資料倉儲、清理和採礦資料，以及管理 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 物件和資料。 這些封裝可單獨使用或搭配其他封裝使用，以因應複雜的商務需求。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 可從各種來源 (如 XML 資料檔案、一般檔案與關聯式資料來源) 擷取與轉換資料，然後再將該資料載入一個或多個目的地。<br /><br /> [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包含一組豐富的內建工作和轉換；建構封裝的工具；以及執行和管理封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務。 您可使用 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 圖形工具建立方案，而不需要撰寫任何程式碼；或者，您也可以撰寫擴充 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 物件模型，以程式設計方式建立封裝及撰寫自訂工作和其他封裝物件。<br /><br /> **依區域瀏覽內容**<br /> ![小型檔案資料夾圖示](media/filefolder-small.gif "小型檔案資料夾圖示")[最新消息](what-s-new-in-integration-services-in-sql-server-2016.md)<br /><br /> ![小型檔案資料夾圖示](media/filefolder-small.gif "小型檔案資料夾圖示")[回溯相容性](integration-services-backward-compatibility.md)<br /><br /> ![小型檔案資料夾圖示](media/filefolder-small.gif "小型檔案資料夾圖示") [Integration Services 功能及工作](../../2014/integration-services/integration-services-features-and-tasks.md)<br /><br /> ![小型檔案資料夾圖示](media/filefolder-small.gif "小型檔案資料夾圖示")[技術參考](../../2014/integration-services/technical-reference-integration-services.md)  
  
 網路廣播：[企業資訊管理 (EIM): 結合使用 SSIS、 DQS 和 MDS](http://go.microsoft.com/fwlink/?LinkId=258672)，channel9.msdn.com 上。  
  
![Integration Services 圖示 （小）](media/dts-16.gif "Integration Services 圖示 （小）")**保持最多 with Integration Services 的日期** <br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
  