---
title: 使用 URL 存取搜尋報表 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- searching reports
- text searches [Reporting Services]
- URL access [Reporting Services], report searches
ms.assetid: 6f3410c4-7944-448f-bae8-bab3e8152d46
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: e0296acddd21319949ff2f76757c5297eb1bceb4
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56023784"
---
# <a name="search-a-report-using-url-access"></a>使用 URL 存取搜尋報表
  您可以使用 URL 存取來搜尋特定文字集的報表。 若要搜尋報表，請在 URL 上將 *rc:FindString* 參數的值設定為等於您要搜尋的文字。 此外，請使用 *rc:StartFind* 和 *rc:EndFind* 參數，將搜尋縮小到報表內的特定頁面。  
  
## <a name="example"></a>範例  
 下列的 URL 存取範例會在 Product Catalog 範例報表中搜尋第一個出現的 "Mountain-400" 文字 (搜尋開始於頁面 1，終止於頁面 5)：  
  
```  
http://server/Reportserver?/SampleReports/Product Catalog&rs:Command=Render&rc:StartFind=1&rc:EndFind=5&rc:FindString=Mountain-400  
```  
  
## <a name="see-also"></a>另請參閱  
 [URL 存取 &#40;SSRS&#41;](url-access-ssrs.md)   
 [URL 存取參數參考](url-access-parameter-reference.md)  
  
  
