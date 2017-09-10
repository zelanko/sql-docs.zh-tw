---
title: "開始使用 Microsoft R Server (獨立式) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: r-server
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 52347d0d-ce60-4bb8-98d2-6163e87716b0
caps.latest.revision: 21
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fc7874c6900474c7c2f3d927183616b2f5e69699
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="getting-started-with-microsoft-r-server-standalone"></a>開始使用 Microsoft R Server (獨立)
  Microsoft R Server (獨立) 可協助您將熱門的開放原始碼 R 語言帶入企業中，以便啟用高效能分析方案以及與其他商務應用程式整合。  

  
## <a name="install-microsoft-r-server"></a>安裝 Microsoft R Server 

您安裝 Microsoft R Server 的方式取決於您是否需要在應用程式中使用 SQL Server 資料。 如果需要，您應該使用 SQL Server 安裝程式來安裝。 如果您將不使用 SQL Server 資料，或是不需要在資料庫內執行 R 程式碼，則可以使用 SQL Server 安裝程式或新的獨立安裝程式。
 
 
+ 從 SQL Server 安裝程式安裝 Microsoft R Server (獨立式)。 系統會為 R Server 建立個別的 R 二進位檔執行個體，並透過 SQL Server Enterprise Edition 支援原則來授權執行個體。 如需詳細資訊，請參閱[建立獨立式 R Server](../../advanced-analytics/r-services/create-a-standalone-r-server.md)。  

+ 使用新的獨立 Windows 安裝程式，以建立使用「Microsoft 新式軟體生命週期」支援原則的全新 Microsoft R Server 執行個體。 如需詳細資訊，請參閱[執行 Microsoft R Server for Windows (英文)](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)。

+ 如果您有想要升級的現有 R Server (獨立式) 或 R Services 執行個體，則您也必須下載並執行 Windows 型安裝程式，才能進行更新。 如需詳細資訊，請參閱[執行 Microsoft R Server for Windows (英文)](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)。
  
## <a name="install-additional-r-tools"></a>安裝其他 R 工具  

 建議您使用免費的 [Microsoft R Client](http://aka.ms/rclient/download) (下載)。  

 您也可以使用慣用的 R 開發環境來為 SQL Server R Services 或 Microsoft R Server 開發方案。 如需詳細資料，請參閱[安裝或設定 R 工具](../../advanced-analytics/r-services/setup-or-configure-r-tools.md)。 
 

### <a name="location-of-r-server-binaries"></a>R Server 二進位檔的位置

依據您安裝 Microsoft R Server 之方式的不同，預設位置也會不同。 在您開始使用您最喜歡的開發環境之前，請先確認您的 R 程式庫安裝位置：

+ 使用新的 Windows 安裝程式來安裝的 Microsoft R Server

  `C:\Program Files\Microsoft\R Server\R_SERVER`

+ 透過 SQL Server 安裝程式來安裝的 R Server (獨立式)

  `C:\Program Files\Microsoft SQL Server\130\R_SERVER`

+ R 服務 (資料庫內)

  `C:\Program Files\Microsoft SQL Server\<instance_name>\R_SERVICES`
      
## <a name="start-using-r-on-microsoft-r-server"></a>開始在 Microsoft R Server 上使用 R  

 設定完伺服器元件並已設定 R IDE 以使用 R Server 二進位檔之後，您便可以開始使用新的 API (例如 RevoScaleR 套件、MicrosoftML 及 olapR) 來開發方案。
    
若要開始使用 R Server，請參閱 MSDN Library 中的這份指南：[R Server - 入門 (英文)](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node)   
  
-   [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-getting-started)：探索這個為 R 方案提供高效能和延展性的可散布分析函數集合。 包含許多最熱門 R 模型建立套件 (例如 	K-Means 叢集、決策樹及決策樹系) 的可平行處理版本，以及資料操作工具。 如需詳細資訊，請參閱[以 25 種函數探索 R 和 ScaleR (英文)](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started-tutorial)  
    
- [MicrosoftML](https://msdn.microsoft.com/library/mt790482.aspx)：MicrosoftML 套件是一組在 Microsoft 開發的新機器學習演算法和轉換，不僅運作快速且可調整。 如需詳細資訊，請參閱 [MicrosoftML 函數 (英文)](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml)。
  


  
## <a name="see-also"></a>另請參閱  
 [開始使用 SQL Server R 服務](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
  
  

