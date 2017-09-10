---
title: "轉散發 ADOMD.NET |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- ADOMD.NET, redistributing
- redistributing ADOMD.NET
ms.assetid: f8db3c99-0243-4b92-b486-0d8786c264f4
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3851f8dd3eea3fb2a98554bba365e723765a641d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="redistributing-adomdnet"></a>轉散發 ADOMD.NET
  當您撰寫使用 ADOMD.NET 的應用程式時，必須連同應用程式一起轉散發適當版本的 ADOMD.NET。 若要轉散發 ADOMD.NET，請將 ADOMD.NET 安裝程式包含在應用程式的安裝程式內。  
  
 ADOMD.NET 安裝程式和最新版本的 ADOMD.NET 屬於 SQL Server 功能套件的一部分，可以在 Microsoft 下載中心找到。  
  
 將 ADOMD.NET 安裝程式中安裝 ADOMD.NET 檔案中的\<*系統磁碟機*>: \Program Files\Microsoft.NET\ADOMD.NET\\*版本號碼*。  
  
 將 ADOMD.NET 安裝程式包含在內之後，讓應用程式的安裝程式啟動 ADOMD.NET 安裝程式並安裝 ADOMD.NET。 此外，視您的環境而定，您可能需要確保相關組件已受 SQL Server 所信任。  
  
 如需詳細資訊：＜＞  
  
 [Microsoft SQL Server 功能套件](http://go.microsoft.com/fwlink/?LinkId=389949)  
  
 [Microsoft Connect: ADOMD.NET 相依性](http://go.microsoft.com/fwlink/?LinkId=389950)  
  
## <a name="see-also"></a>另請參閱  
 [ADOMD.NET 用戶端程式設計](../../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)   
 [ADOMD.NET 伺服器程式設計](../../../analysis-services/multidimensional-models-adomd-net-server/adomd-net-server-programming.md)  
  
  
