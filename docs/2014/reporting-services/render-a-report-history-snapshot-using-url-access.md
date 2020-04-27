---
title: 使用 URL 存取轉譯報表記錄快照集 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- URL access [Reporting Services], report history
- history snapshots [Reporting Services]
- historical data [Reporting Services]
- snapshots [Reporting Services], URL access
- snapshots [Reporting Services], rendering report history
ms.assetid: 3f87f82d-0e61-4492-9c4b-f5238c39e8cd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 67854a39ab7e38289627d03ac00cc4b2a6dca6f2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66107974"
---
# <a name="render-a-report-history-snapshot-using-url-access"></a>使用 URL 存取轉譯報表記錄快照集
  您可以提供 *rs:Snapshot* 參數並將其值設定為有效的快照集識別碼，來根據報表記錄快照集轉譯報表。 參數值的格式是 YYYY-MM-DDTHH:MM:SS，此格式符合國際標準組織 (ISO) 8601 標準。  
  
 如果您省略此參數，就會根據報表伺服器的報表執行與快取管理選項設定來轉譯報表。 如需報表執行的詳細資訊，請參閱 [設定報表處理屬性](report-server/set-report-processing-properties.md)。  
  
## <a name="example"></a>範例  
 下列範例會顯示擷取報表記錄快照集的 URL：  
  
```  
http://myrshost/reportserver?/SampleReports/Company Sales&rs:Snapshot=2003-04-07T13:40:02  
```  
  
## <a name="see-also"></a>另請參閱  
 [URL 存取 &#40;SSRS&#41;](url-access-ssrs.md)   
 [URL 存取參數參考](url-access-parameter-reference.md)  
  
  
