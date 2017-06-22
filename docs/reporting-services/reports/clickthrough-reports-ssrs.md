---
title: "點選連結報表 (SSRS) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- clickthrough reports
- customizing clickthrough reports
- clickthrough reports, customizing
ms.assetid: cf2c396e-b0c6-41f9-8c45-ddc8406f7e85
caps.latest.revision: 28
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 55d22d2fd64faef6e913bf226c831546d71665ca
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="clickthrough-reports-ssrs"></a>點選連結報表 (SSRS)
  點選連結報表是一個提供有關主報表所含資料之詳細資訊的報表。 當使用者按一下出現在主報表中的互動式資料時，就會顯示點選連結報表。 報表伺服器會自動產生這些報表。 模型設計師必須設定指派給報表模型中實體的 **DefaultDetailAttribute** 和 **DefaultAggregateAttribute** 屬性，以決定要在點選連結報表中顯示的內容。  
  
> [!NOTE]  
>  並非 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的所有版本都可使用點選連結報表。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本支援的功能清單，請參閱 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。 如果不確定您的組織執行哪個版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請連絡資料庫管理員。  
  
## <a name="using-default-templates"></a>使用預設範本  
 依預設，報表伺服器會為每個實體產生兩種 clickthrough 範本類型：單一執行個體範本和多執行個體範本。 您所按的項目會決定所用的範本。 如果讀取報表的人按一下純量屬性，則會使用單一執行個體範本。 如果讀取報表的人按一下彙總屬性，則會使用多執行個體範本。  
  
#### <a name="single-instance-templates"></a>單一執行個體範本  
 單一執行個體範本會顯示目標實體的所有屬性，並顯示從目標實體為具有一對多關係之相關實體指定的所有預設彙總屬性。 單一執行個體範本的外觀類似下圖。  
  
 ![多對 1 點選連結報表。](../../reporting-services/reports/media/manytooneclickthrough.gif "多對 1 點選連結報表。")  
  
#### <a name="multiple-instance-templates"></a>多執行個體範本  
 多執行個體範本只顯示目標實體的預設詳細屬性，以及從目標實體為具有一對多關係之相關實體指定的所有預設彙總屬性。 多執行個體範本的外觀類似下圖。  
  
 ![多對 1 點選連結報表。](../../reporting-services/reports/media/onetomanyclickthrough.gif "多對 1 點選連結報表。")  
  
## <a name="customizing-clickthrough-reports"></a>自訂點選連結報表  
 如果不使用報表伺服器產生的預設範本，您可以在報表產生器中建立報表，然後以它作為自訂點選連結報表。 然後，您就可以在報表管理員中，將報表連結至模型當做體鑽研報表。  
  
 若要將報表產生器報表轉換為點選連結報表，您必須在報表產生器 [屬性] 對話方塊中選取 [啟用鑽研此報表] 選項。 選取此選項之後，鑽研參數就會加入該報表中，因而無法再直接於報表產生器中執行該報表。 當報表讀者按一下報表產生器報表中的項目時，報表伺服器會自動計算鑽研參數。  
  
> [!IMPORTANT]  
>  報表中使用的主要實體或基底實體，必須與連結報表的實體相同。  
  
## <a name="see-also"></a>請參閱＜  
 [將報表連結至模型以做為點選連結報表](http://msdn.microsoft.com/library/3af42de3-67ef-41c2-bc8a-7045baec6f63)  
  
  

