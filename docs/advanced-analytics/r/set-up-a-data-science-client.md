---
title: "設定資料科學用戶端 | Microsoft Docs"
ms.custom: 
ms.date: 02/10/2017
ms.prod: r-server
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d15ee956-918f-40e0-b986-2bf929ef303a
caps.latest.revision: 14
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0661b2fcf9b23d3c81cb0d80f0424d87dbde7ef8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="set-up--a-data-science-client"></a>設定資料科學用戶端
  在藉由安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] R Services (資料庫內) **以設定**執行個體之後，您會想要為遠端執行和部署設定能夠連接到伺服器的 R 開發環境。 
  
  此環境必須包含 ScaleR 套件，且可以選擇性地包含用戶端開發環境。
  
 ## <a name="where-to-get-scaler"></a>何處可以取得 ScaleR 
  
  用戶端環境必須包含 Microsoft R Open，以及支援在 SQL Server 上分散式執行 R 的其他 RevoScaleR 套件。  您有數種方式可以安裝這些套件︰
  
+ 安裝 [Microsoft R Client](http://aka.ms/rclient/download)。 這裡提供其他安裝指示：[開始使用 Microsoft R 用戶端 (英文)](https://msdn.microsoft.com/microsoft-r/r-client-get-started)
+ 安裝 Microsoft R Server。 您可從 SQL Server 安裝程式或使用新的 Windows 獨立安裝程式，取得 Microsoft R Server。 如需詳細資訊，請參閱[建立獨立的 R Server](../../advanced-analytics/r-services/create-a-standalone-r-server.md) 和 [R Server 簡介 (英文)](https://msdn.microsoft.com/microsoft-r/rserver)。

如果您擁有 R Server 授權合約，我們建議您使用 Microsoft R Server (獨立)，以避免 R 處理執行序和記憶體內資料的限制。


## <a name="how-to-set-up-the-r-development-environment"></a>如何設定 R 開發環境

您可以選擇使用任何與 Windows 相容的 R 開發環境。 

+ 適用於 Visual Studio 的 R Tools 支援與 Microsoft R Open 整合
+ RStudio 是受歡迎的免費環境  

安裝之後，您會需要重新設定您的環境，以使用預設的 Microsoft R Open 程式庫，否則您無法存取 ScaleR 函數庫。 如需詳細資訊，請參閱[開始使用 Microsoft R 用戶端 (英文)](http://msdn.microsoft.com/microsoft-r/r-client-get-started)。
 
## <a name="more-resources"></a>其他資源
  
 如需如何連接到遠端執行 R 程式碼之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的詳細逐步解說，請參閱本教學課程︰ [資料科學深入探討︰使用 RevoScaleR 套件](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)。  
 

若要開始 SQL Server 使用 Microsoft R 用戶端和 ScaleR 套件，請參閱[開始使用 ScaleR (英文)](https://msdn.microsoft.com/microsoft-r/scaler-getting-started#)。  
  
## <a name="see-also"></a>另請參閱  
 [設定 SQL Server R Services &#40;資料庫內&#41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)  
  
  

