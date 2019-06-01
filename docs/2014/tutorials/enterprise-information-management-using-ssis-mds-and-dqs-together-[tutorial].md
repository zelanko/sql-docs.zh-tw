---
title: 使用 SSIS、 MDS 和 DQS 一起 [教學課程] 的企業資訊管理 |Microsoft Docs
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
ms.openlocfilehash: 61773674412a8b4bdd8b5fa2f8b207de66254dcc
ms.sourcegitcommit: 5905c29b5531cef407b119ebf5a120316ad7b713
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/31/2019
ms.locfileid: "66429031"
---
# <a name="enterprise-information-management-using-ssis-mds-and-dqs-together-tutorial"></a>使用 SSIS、MDS 和 DQS 一起管理企業資訊 [教學課程]
  管理企業的資訊通常牽涉到整合整個企業及外部的資料、清理資料、比對資料來移除任何重複項、標準化資料、充實資料，使資料符合法律和規範要求，然後將資料儲存在集中位置，並具有所有必要的安全性設定。  
  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 在單一產品中提供了有效企業資訊管理 (EIM) 解決方案所需的所有元件。 可幫助您建置 EIM 解決方案的主要元件包括：  
  
-   SQL Server Integration Services  
  
-   SQL Server Data Quality Services  
  
-   SQL Server Master Data Services  
  
 SQL Server Integration Services (SSIS) 提供了功能強大而且可擴充的平台，透過全面性擷取、轉換和載入 (ETL) 解決方案從各種不同的來源整合資料，這個解決方案可支援商務工作流程、資料倉儲或主要資料管理。 請參閱[Integration Services 概觀](https://msdn.microsoft.com/library/ms141263\(SQL.105\).aspx)取得快速概觀和典型的主題使用的 SSIS。  
  
 SQL Server Data Quality Services (DQS) 可讓您清理、比對、標準化及充實資料，好讓您可以針對商業智慧、資料倉儲和交易處理工作負載傳遞可靠的資訊。 請參閱[Data Quality Services 簡介](https://msdn.microsoft.com/library/ff877917.aspx)DQS 及 DQS 如何回應需求的商務需求的主題。  
  
 SQL Server Master Data Services (MDS) 提供一個資料中樞，可確保資訊的完整性和資料的一致性在不同應用程式之間都保持不變。 請參閱[Master Data Services 概觀](../master-data-services/master-data-services-overview-mds.md)MDS 的重要功能的簡短描述的主題。  
  
 請參閱[清理和比對主要資料的使用 EIM 技術](https://msdn.microsoft.com/library/hh403491.aspx)實作 EIM 解決方案一起使用這些 Microsoft EIM 技術和監看式的全面性指引的技術白皮書[Enterprise資訊管理 (EIM):結合使用 SSIS、 DQS 和 MDS](https://go.microsoft.com/fwlink/?LinkId=258672) EIM 案例的示範影片。  
  
 在本教學課程中，您會學習如何一起使用 SSIS、MDS 和 DQS 來實作範例企業資訊管理 (EIM) 解決方案。 首先，您會使用 DQS 來建立包含資料 (中繼資料) 相關知識的知識庫、使用知識庫清理 Excel 檔案中的資料，並且比對資料來識別及移除資料的重複項。 接下來，您會使用適用於 Excel 的 MDS 增益集，將已清理和比對的資料上傳至 MDS。 然後，您會使用 SSIS 解決方案自動化整個程序。 本教學課程的 SSIS 解決方案會從 Excel 檔案讀取輸入資料，但是您可以將它擴充，以便從各種不同的來源讀取，例如 Oracle、Teradata、DB2 和 Windows Azure SQL Database。  
  
## <a name="prerequisites"></a>先決條件  
  
1.  已安裝下列元件的 Microsoft SQL Server 2012。  
  
    1.  Integration Services (SSIS)  
  
    2.  Master Data Services (MDS)  
  
    3.  Data Quality Services (DQS)  
  
    4.  SQL Server Data Tools  
  
         請參閱[SQL Server 2012 安裝指南](../database-engine/install-windows/installation-for-sql-server.md)如需安裝產品詳細資料。  
  
2.  [設定 MDS 使用 Master Data Services 組態管理員](https://msdn.microsoft.com/library/ee633884.aspx)  
  
     使用組態管理員建立及設定 Master Data Services 資料庫。 建立 MDS 資料庫之後，為 MDS 建立 web 應用程式中的網站 (例如： [ http://localhost/MDS ](http://localhost/MDS)) 並將 MDS 資料庫與 MDS web 應用程式產生關聯。 請注意，若要建立 MDS Web 應用程式，您的電腦上應該已安裝 IIS。 請參閱[Web 應用程式需求 (Master Data Services)](https://msdn.microsoft.com/library/ee633744.aspx)並[資料庫需求 (Master Data Services)](https://msdn.microsoft.com/library/ee633767.aspx)設定 MDS 資料庫與 web 應用程式的必要條件的詳細資料。  
  
3.  [安裝和設定 DQS 使用 Data Quality Server Installer](https://msdn.microsoft.com/library/hh231682.aspx)。 按一下 **開始**，按一下**所有程式**，按一下  **Microsoft SQL Server 2014**，按一下  **Data Quality Services**，然後按一下**Data Quality Server Installer**。  
  
4.  Microsoft Excel 2010 (慣用 32 位元版本)。  
  
5.  安裝**Master Data Services 增益集適用於 Excel** （32 位元或 64 位元根據您的電腦必須有的 Excel 的版本） 從[這裡](https://www.microsoft.com/download/details.aspx?id=29064)。 若要尋找的電腦上安裝的 Excel 版本，請執行**Excel**，按一下**檔案**功能表列，然後按一下 **協助**以查看右窗格中的版本。 請注意，您需要安裝 Visual Studio 2010 Tools for Office Runtime，再安裝 Excel 增益集。  
  
6.  （選擇性）建立具有的帳戶[Windows Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/)。 其中一個教學課程中的工作必須要有**Azure Marketplace** (最初稱為**Data Market**) 帳戶。 如果您想要可以略過此工作，並繼續進行下一項工作。  
  
7.  下載 Suppliers.xls 檔案從[Microsoft 下載中心](https://www.microsoft.com/download/details.aspx?id=50426)。  
  
8.  DQS 不允許您將清理或比對到 Excel 檔案的結果，如果您使用匯出**64 位元版本的 Excel**。 這是已知的問題。 若要解決此問題，請執行以下步驟：  
  
    1.  執行**DQLInstaller.exe-升級**。 如果已經安裝了 SQL Server 的預設執行個體，DQSInstaller.exe 檔案將會位於 C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn。 按兩下 DQSInstaller.exe 檔案。  
  
    2.  在**Master Data Services 組態管理員**，按一下**選取資料庫**、 選取現有**MDS**資料庫，然後再按一下**升級**.  
  
## <a name="lessons"></a>課程  
  
|課程|簡短描述|完成的估計時間 (以分鐘計)。|  
|------------|-----------------------|------------------------------------------------|  
|[第 1 課：建立供應商 DQS 知識庫](../../2014/tutorials/lesson-1-creating-the-suppliers-dqs-knowledge-base.md)|在這一課，您會建立名為 DQS 知識庫**供應商**。|60|  
|[第 2 課：使用供應商知識庫清理供應商資料](../../2014/tutorials/lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base.md)|在這一課中，建立並執行 DQS 專案來清理 Excel 檔案中的供應商資料使用**供應商**您在第 1 課中建立的知識庫。|45|  
|[第 3 課：比對資料來移除重複項目從供應商清單](../../2014/tutorials/lesson-3-matching-data-to-remove-duplicates-from-supplier-list.md)|在這一課，您會建立 DQS 專案來執行比對活動，以識別及移除已清理之供應商清單中的重複項。|45|  
|[第 4 課：在 MDS 中儲存供應商資料](../../2014/tutorials/lesson-4-storing-supplier-data-in-mds.md)|在這一課，您將資料上傳已清理和比對的供應商到 Master Data Services (MDS) 使用**MDS 增益集適用於 Excel**。|45|  
|[第 5 課：自動化清理和比對使用 SSIS](../../2014/tutorials/lesson-5-automating-the-cleansing-and-matching-using-ssis.md)|在這一課，您會使用 DQS 來建立可清理輸入資料的 SSIS 解決方案、比對已清理的資料來移除重複項，並以自動化方式將已清理和比對的資料儲存在 MDS 上。|75|  
  
## <a name="next-steps"></a>後續步驟  
 若要開始本教學課程，請繼續進行第 1 課：[第 1 課：建立供應商 DQS 知識庫](../../2014/tutorials/lesson-1-creating-the-suppliers-dqs-knowledge-base.md)。  
  
  
