---
title: 將 SSIS、MDS 和 DQS 結合使用的企業資訊管理 [教程] |微軟文件
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ba09b504-3007-4cb7-8ef8-f01adbf51646
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 29ed5816a3a5fc0af6c5a4ac144557933e3e1a5f
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487717"
---
# <a name="enterprise-information-management-using-ssis-mds-and-dqs-together-tutorial"></a>使用 SSIS、MDS 和 DQS 一起管理企業資訊 [教學課程]
  管理企業的資訊通常牽涉到整合整個企業及外部的資料、清理資料、比對資料來移除任何重複項、標準化資料、充實資料，使資料符合法律和規範要求，然後將資料儲存在集中位置，並具有所有必要的安全性設定。  
  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 在單一產品中提供了有效企業資訊管理 (EIM) 解決方案所需的所有元件。 可幫助您建置 EIM 解決方案的主要元件包括：  
  
-   SQL Server Integration Services  
  
-   SQL Server Data Quality Services  
  
-   SQL Server Master Data Services  
  
 SQL Server Integration Services (SSIS) 提供了功能強大而且可擴充的平台，透過全面性擷取、轉換和載入 (ETL) 解決方案從各種不同的來源整合資料，這個解決方案可支援商務工作流程、資料倉儲或主要資料管理。 有關 SSIS 的快速概述和典型用途,請參閱[整合服務概述](https://msdn.microsoft.com/library/ms141263\(SQL.105\).aspx)主題。  
  
 SQL Server Data Quality Services (DQS) 可讓您清理、比對、標準化及充實資料，好讓您可以針對商業智慧、資料倉儲和交易處理工作負載傳遞可靠的資訊。 有關 DQS 的業務需求以及 DQS 如何滿足需求,請參閱[介紹數據服務品質主題](https://msdn.microsoft.com/library/ff877917.aspx)。  
  
 SQL Server Master Data Services (MDS) 提供一個資料中樞，可確保資訊的完整性和資料的一致性在不同應用程式之間都保持不變。 有關 MDS 重要功能的簡要說明,請參閱[主數據服務概述](../master-data-services/master-data-services-overview-mds.md)主題。  
  
 請參閱[使用 EIM 技術白皮書清理和匹配主數據](https://msdn.microsoft.com/library/hh403491.aspx),瞭解有關使用這些 Microsoft EIM 技術實現 EIM 解決方案的全面指南,並觀看[企業資訊管理 (EIM):將 SSIS、DQS 和 MDS 視頻整合在一起](https://go.microsoft.com/fwlink/?LinkId=258672),以便對 EIM 方案進行冷靜演示。  
  
 在本教學課程中，您會學習如何一起使用 SSIS、MDS 和 DQS 來實作範例企業資訊管理 (EIM) 解決方案。 首先，您會使用 DQS 來建立包含資料 (中繼資料) 相關知識的知識庫、使用知識庫清理 Excel 檔案中的資料，並且比對資料來識別及移除資料的重複項。 接下來，您會使用適用於 Excel 的 MDS 增益集，將已清理和比對的資料上傳至 MDS。 然後，您會使用 SSIS 解決方案自動化整個程序。 本教學中的 SSIS 解決方案從 Excel 檔讀取輸入資料,但您可以將其擴展到從 Oracle、Teradata、DB2 和 Azure SQL 資料庫等各種源讀取。  
  
## <a name="prerequisites"></a>Prerequisites  
  
1.  已安裝下列元件的 Microsoft SQL Server 2012。  
  
    1.  Integration Services (SSIS)  
  
    2.  Master Data Services (MDS)  
  
    3.  Data Quality Services (DQS)  
  
    4.  SQL Server Data Tools  
  
         有關安裝產品的詳細資訊,請參閱[SQL Server 2012 安裝指南](../database-engine/install-windows/installation-for-sql-server.md)。  
  
2.  [使用 Master Data Services 組態管理員設定 MDS](https://msdn.microsoft.com/library/ee633884.aspx)  
  
     使用組態管理員建立及設定 Master Data Services 資料庫。 創建 MDS 資料庫後,在 Web 網站中為`http://localhost/MDS`MDS 創建 Web 應用程式(例如: ),並將 MDS 資料庫與 MDS Web 應用程式相關聯。 請注意，若要建立 MDS Web 應用程式，您的電腦上應該已安裝 IIS。 有關配置 MDS 資料庫和 Web 應用程式的先決條件的詳細資訊,請參閱[Web 應用程式要求(主資料服務)](https://msdn.microsoft.com/library/ee633744.aspx)和[資料庫要求(主資料服務)。](https://msdn.microsoft.com/library/ee633767.aspx)  
  
3.  [使用數據品質伺服器安裝程式安裝和配置DQS。](https://msdn.microsoft.com/library/hh231682.aspx) 點選 **「開始」** 選**單擊 所有程式**,按下**Microsoft SQL Server 2014**,按下**資料品質服務**,然後按下**資料品質伺服器安裝程式**。  
  
4.  Microsoft Excel 2010 (慣用 32 位元版本)。  
  
5.  [從這裡](https://www.microsoft.com/download/details.aspx?id=29064)安裝**Excel 的主資料服務外接程式**(基於電腦上的 Excel 版本的 32 位元或 64 位)。 要查找電腦上安裝的 Excel 版本,請運行**Excel,** 按下選單列上的 **「檔**」,然後單擊 **「説明**」以查看右側窗格中的版本。 請注意，在您安裝 Excel 增益集之前，您必須先安裝 Visual Studio 2010 Tools for Office Runtime。  
  
6.  ( 選擇性的 )使用 Azure[應用商店](https://azuremarketplace.microsoft.com/marketplace/)創建帳戶。 本教程中的一項任務要求您具有**Azure 應用商店**(最初稱為**數據市場**)帳戶。 如果您想要可以略過此工作，並繼續進行下一項工作。  
  
7.  從[微軟下載中心](https://www.microsoft.com/download/details.aspx?id=50426)下載供應商.xls檔。  
  
8.  如果使用**64 位元版本的 Excel**,則 DQS 不允許將清理結果或匹配結果匯出到 Excel 檔。 這是已知的問題。 若要解決此問題，請執行以下步驟：  
  
    1.  執行**DQL 安裝程式.exe -升級**。 如果已經安裝了 SQL Server 的預設執行個體，DQSInstaller.exe 檔案將會位於 C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn。 按兩下 DQSInstaller.exe 檔案。  
  
    2.  在**主資料服務設定管理器**中,按下 **「選擇資料庫**」,選擇現有的**MDS**資料庫,然後單擊「**升級**」 。。  
  
## <a name="lessons"></a>課程  
  
|課程|簡短描述|完成的估計時間 (以分鐘計)。|  
|------------|-----------------------|------------------------------------------------|  
|[第 1 課：建立供應商 DQS 知識庫](../../2014/tutorials/lesson-1-creating-the-suppliers-dqs-knowledge-base.md)|在本課中,您將創建名為「**供應商」的**DQS 知識庫。|60|  
|[第 2 課：使用供應商知識庫清理供應商資料](../../2014/tutorials/lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base.md)|在本課中,您將創建並運行一個 DQS 專案,透過使用您在第一課中創建的**供應商**知識庫清理 Excel 檔案中的供應商數據。|45|  
|[第 3 課：比對資料，以便從供應商清單中移除重複項](../../2014/tutorials/lesson-3-matching-data-to-remove-duplicates-from-supplier-list.md)|在這一課，您會建立 DQS 專案來執行比對活動，以識別及移除已清理之供應商清單中的重複項。|45|  
|[第 4 課：在 MDS 中儲存供應商資料](../../2014/tutorials/lesson-4-storing-supplier-data-in-mds.md)|在本課中,您可以使用用於 Excel 的**MDS 外接程式**將清理和匹配的供應商數據上載到主數據服務 (MDS)。|45|  
|[第 5 課：使用 SSIS 將清理和比對自動化](../../2014/tutorials/lesson-5-automating-the-cleansing-and-matching-using-ssis.md)|在這一課，您會使用 DQS 來建立可清理輸入資料的 SSIS 解決方案、比對已清理的資料來移除重複項，並以自動化方式將已清理和比對的資料儲存在 MDS 上。|75|  
  
## <a name="next-steps"></a>後續步驟  
 首先,請繼續學習第一課:第[1 課:創建供應商 DQS 知識庫](../../2014/tutorials/lesson-1-creating-the-suppliers-dqs-knowledge-base.md)。  
  
  
