---
title: 轉散發 ADOMD.NET |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: adomd
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5e3a563c5c51e4852fd477f9acdbf76e31e80dc8
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
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
  
  
