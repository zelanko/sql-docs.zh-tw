---
title: "SQL Server 文件離線存取 | Microsoft Docs"
ms.custom: 
ms.date: 08/22/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- server-general
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 257ed357-8cbb-43bd-b042-254be5fbb977
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1266b0249a96fbc4828b2afee9fb218682501e4d
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-documentation-offline-access"></a>SQL Server 文件離線存取

離線檢視 SQL Server 2016 技術文件。
  
## <a name="prerequisites"></a>必要條件
若要離線檢視 SQL Server 2016 技術文件，您需要有安裝下列產品的 HelpViewer 2.2： 
- [Visual Studio 2015 (包括 Community 在內的任何版本)](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) ，或
- [SQL Server Management Studio (SSMS) 2016 年 4 月預覽 (13.0.12500.29) 或更新版本](https://msdn.microsoft.com/library/mt238290.aspx)

請安裝任一產品，再繼續進行下列步驟。
  
## <a name="install-sql-server-offline-technical-documentation"></a>安裝 SQL Server 離線技術文件 

1. 安裝任何 Visual Studio 2015 版本或 SSMS 2016 年 4 月預覽組建或更新版本。 
2. 啟動 SSMS 或 Visual Studio。
3. 從上方導覽列的 [說明]**** 功能表中，選取 [加入和移除說明內容]****。 

#### <a name="this-action-launches-the-helpviewer"></a>(此動作會啟動 HelpViewer)

4. 在 HelpViewer 中，選擇預設安裝來源︰**線上** 
5. 按一下您要安裝之所有文件旁的 [加入]****。
6. 按一下畫面右下方的 [更新]**** 按鈕，下載並安裝您選取的文件。
![載入離線內容](../sql-server/media/load-offline-content.png) 

 >** 重要！！** 按一下 [更新] 之後，HelpViewer 最終將凍結/停止回應。 它仍會下載並安裝好您選擇的文件。 **若要解決此問題**，請在 [工作管理員] 中結束 HelpViewer，然後遵循上述步驟 3 將它重新啟動。 HelpViewer 第一次凍結/停止回應時，也請遵循 [這些步驟](https://msdn.microsoft.com/library/mt654096.aspx) 。 您只需要執行這些步驟一次，但您可能需要在每次更新內容時，從 [工作管理員] 中結束 HelpViewer。  
6. 再次選取[說明]/[加入和移除內容]，重新啟動 HelpViewer。 您的離線文件現在可供使用！



   ![準備離線使用](../sql-server/media/offline-ready-to-use.png)




