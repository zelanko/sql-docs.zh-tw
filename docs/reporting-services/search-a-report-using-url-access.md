---
title: "使用 URL 存取搜尋報表 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- searching reports
- text searches [Reporting Services]
- URL access [Reporting Services], report searches
ms.assetid: 6f3410c4-7944-448f-bae8-bab3e8152d46
caps.latest.revision: "34"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 6de1f0cb87292513b0765a5653ce1cabcacdf105
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="search-a-report-using-url-access"></a>使用 URL 存取搜尋報表
  您可以使用 URL 存取來搜尋特定文字集的報表。 若要搜尋報表，請在 URL 上將 *rc:FindString* 參數的值設定為等於您要搜尋的文字。 此外，請使用 *rc:StartFind* 和 *rc:EndFind* 參數，將搜尋縮小到報表內的特定頁面。  
  
## <a name="example"></a>範例  
 下列的 URL 存取範例會在 Product Catalog 範例報表中搜尋第一個出現的 "Mountain-400" 文字 (搜尋開始於頁面 1，終止於頁面 5)：  
  
```  
http://server/Reportserver?/SampleReports/Product Catalog&rs:Command=Render&rc:StartFind=1&rc:EndFind=5&rc:FindString=Mountain-400  
```  
  
## <a name="see-also"></a>另請參閱  
 [URL 存取 &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [URL 存取參數參考](../reporting-services/url-access-parameter-reference.md)  
  
  
