---
title: "匯入和匯出知識 | Microsoft Docs"
ms.custom: 
ms.date: 07/31/2012
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 12537c9d-31e4-40b0-a411-cb343abbe96a
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a0963e7fc98cc0489d6f93c2381b701bd26ef569
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="importing-and-exporting-knowledge"></a>匯入和匯出知識
  您可以直接在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 應用程式中建立知識庫和定義域，也可以將知識匯入知識庫或從中匯出知識。 在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 應用程式中，您可以使用資料檔案進行匯入和匯出作業，或使用 Excel 檔案進行匯入作業。 使用的資料檔案是 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 所建立的加密檔案，副檔名為 .dqs。 由 Microsoft Excel 建立的檔案可以具有 .xlsx、.xls 或 .csv 的副檔名。 這些作業可讓您更有彈性地建置並共用執行資料清理和比對所用的知識。  
  
> [!IMPORTANT]  
>  您可以從命令提示字元執行 DQSInstaller.exe 檔案，一次將 *中的「所有」*[!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 知識庫匯出至 DQS 備份檔案 (.dqsb)。 同樣地，您也可以從命令提示字元執行 DQSInstaller.exe 檔案，一次將 DQS 備份檔案 (.dqsb) 中的「所有」  知識庫匯入 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 中。 如需有關執行此作業的詳細資訊，請參閱《DQS 安裝指南》中的＜ [使用 DQSInstaller.exe 匯出及匯入 DQS 知識庫](../data-quality-services/install-windows/export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md) ＞。  
  
## <a name="in-this-section"></a>本節內容  
 您可以執行下列匯入和匯出作業：  
  
|||  
|-|-|  
|將知識庫中的定義域匯出至 .dqs 資料檔案|[將網域匯出至 .dqs 檔案](../data-quality-services/export-a-domain-to-a-dqs-file.md)|  
|將 .dqs 資料檔案中的定義域匯入現有的知識庫中|[從 .dqs 檔案匯入網域](../data-quality-services/import-a-domain-from-a-dqs-file.md)|  
|將整個知識庫匯出至 .dqs 資料檔案|[將知識匯出至 .dqs 檔案](../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md)|  
|將整個知識庫匯入 .dqs 資料檔案中|[從 .dqs 檔案匯入知識](../data-quality-services/import-a-knowledge-base-from-a-dqs-file.md)|  
|將 Excel 檔案中的值匯入定義域中|[將 Excel 檔案中的值匯入定義域中](../data-quality-services/import-values-from-an-excel-file-into-a-domain.md)|  
|將 Excel 檔案中的定義域匯入知識庫|[將 Excel 檔案中的網域匯入知識探索](../data-quality-services/import-domains-from-an-excel-file-in-knowledge-discovery.md)|  
|將清理期間蒐集的知識匯入知識庫中|[將清理專案值匯入網域](../data-quality-services/import-cleansing-project-values-into-a-domain.md)|  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|藉由執行知識探索以及以互動方式管理知識來建立知識庫|[建置知識庫](../data-quality-services/building-a-knowledge-base.md)|  
|建立單一定義域，並將知識加入至定義域。|[管理網域](../data-quality-services/managing-a-domain.md)|  
|建立複合定義域，並將知識加入至定義域。|[管理複合網域](../data-quality-services/managing-a-composite-domain.md)|  
  
  
