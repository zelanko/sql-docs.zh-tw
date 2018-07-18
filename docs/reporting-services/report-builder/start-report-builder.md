---
title: 啟動報表產生器 | Microsoft Docs
ms.custom: ''
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-builder
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Report Builder, launching
- launching Report Builder
- SharePoint integration [Reporting Services], starting Report Builder
- starting Report Builder
ms.assetid: 8c8c7d2e-b315-418d-bf65-90e7685e4259
caps.latest.revision: 56
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9fd9da00fc99cc47c260c43faa9599b6d2e1d6d3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33020005"
---
# <a name="start-report-builder"></a>啟動報表產生器

[!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 是獨立報表撰寫環境。 您可以使用它來建立分頁報表，以及將它們發行到以原生或 SharePoint 整合模式安裝的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 。  
  
 第一次從 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] Web 入口網站或處於 SharePoint 整合模式的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 時，系統會提示您從 Microsoft 下載中心進行下載。 
 
![report-builder-get-report-builder](../../reporting-services/report-builder/media/report-builder-get-report-builder.png) 
 
 您或系統管理員也可以 [從 Microsoft 下載中心將報表產生器安裝在電腦上](http://go.microsoft.com/fwlink/?LinkID=219138)。 如需詳細資訊，請參閱 [安裝報表產生器](../../reporting-services/install-windows/install-report-builder.md) 中的＜使用系統管理員伺服器安裝報表產生器＞。
 
 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 不是在安裝 SQL Server Reporting Services 時安裝；您需要另外進行下載與安裝。  
  
 從 Web 入口網站或 SharePoint 網站啟動 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 時，如果開啟舊版 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] ，請連絡可更新 Web 入口網站或 SharePoint 網站上版本的系統管理員。  
  
## <a name="to-start-includessrbnoversionincludesssrbnoversion-mdmd-from-the-includessrsnoversionincludesssrsnoversion-mdmd-web-portal"></a>從 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] Web 入口網站啟動 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
1.  在網頁瀏覽器的網址列中，輸入報表伺服器的 URL。 根據預設，URL 為 http://\<*伺服器名稱*>/reports。  
  
2.  在 Web 入口網站的頂端列中，選取 [新增] > [編頁報表]。  
  
     ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png "PBI_SSMRP_NewMenu")  
  
     第一次，系統會提示您 [安裝報表產生器](../../reporting-services/install-windows/install-report-builder.md)。 
  
     之後， [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 隨即開啟，而且您可以從報表伺服器中建立分頁報表或開啟報表。  
  
## <a name="to-start-includessrbnoversionincludesssrbnoversion-mdmd-in-sharepoint-integrated-mode"></a>以 SharePoint 整合模式啟動 [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]  
  
1.  巡覽至包含您需要之文件庫的 SharePoint 網站。  
  
2.  開啟文件庫。  
  
3.  按一下 [文件]。  
  
4.  在 [新增文件] 功能表上，按一下 [報表產生器報表]。  
  
     第一次時，這會啟動 [SQL Server [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 精靈]。 如需詳細資訊，請參閱 [安裝報表產生器](../../reporting-services/install-windows/install-report-builder.md) 。  
  
     [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] 隨即開啟，而且您可以在報表伺服器上建立分頁報表或開啟報表。  
  
     **注意**：如果 [新增文件] 功能表未列出 [報表產生器報表]、[報表產生器模型] 或 [報表資料來源]，則必須將其內容類型加入至 SharePoint 文件庫。 如需詳細資訊，請參閱 [將 Reporting Services 內容類型加入至 SharePoint 文件庫](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)。  

## <a name="next-steps"></a>後續步驟

[SQL Server 2016 的報表產生器](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md)   
[設定報表產生器的預設選項](../../reporting-services/report-builder/set-default-options-for-report-builder.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
