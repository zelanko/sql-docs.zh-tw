---
title: "資料流目的地 |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 640e6a19-49ae-4ee8-ac07-008370158f0e
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3e95b4d887bea5783be935a40877d590b8e8dcff
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="data-streaming-destination"></a>資料流目的地
  **資料流目的地** 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (SSIS) 目的地元件，可讓 **OLE DB Provider for SSIS** 取用 SSIS 封裝的輸出做為表格式結果集。 您可以建立連結的伺服器來使用 OLE DB Provider for SSIS，然後在連結的伺服器上執行 SQL 查詢來顯示 SSIS 封裝所傳回的資料。  
  
 在下列範例中，下列查詢會在 SSIS 目錄的 Power BI 資料夾中，傳回 SSISPackagePublishing 專案的 Package.dtsx 封裝輸出。 此查詢會使用名為 [Integration Services 的預設連結伺服器] 的連結伺服器，接著使用新的 OLE DB Provider for SSIS。 此查詢包括 SSIS 目錄中的資料夾名稱、專案名稱和封裝名稱。 OLE DB Provider for SSIS 會執行您在查詢中指定的封裝，然後傳回表格式結果集。  
  
```  
SELECT * FROM OPENQUERY([Default Linked Server for Integration Services], N'Folder=Power BI;Project=SSISPackagePublishing;Package=Package.dtsx')  
  
```  
  
## <a name="data-feed-publishing-components"></a>資料摘要發行元件  
 資料摘要發行元件包括下列元件︰OLE DB Provider for SSIS、資料流目的地和 SSIS 封裝發行精靈。 此精靈可讓您發行 SSIS 封裝做為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫執行個體中的 SQL 檢視。 此精靈會協助您建立連結的伺服器來使用 OLE DB Provider for SSIS，以及一個 SQL 檢視來表示連結伺服器上的查詢。 您可以執行檢視，來查詢 SSIS 封裝的結果做為表格式資料集。  
  
 若要確認 SSISOLEDB 提供者已安裝，可在 SQL Server Management Studio 中，展開 [伺服器物件] 、[連結的伺服器] 、[提供者] ，然後確認您看到 **SSISOLEDB** 提供者。 按兩下 [SSISOLEDB]、啟用 [允許 Inprocess] (若未啟用)，然後按一下 [確定]。  
  
## <a name="publish-an-ssis-package-as-a-sql-view"></a>發行 SSIS 封裝做為 SQL 檢視  
 下列程序說明發行 SSIS 封裝做為 SQL 檢視的步驟。  
  
1.  使用 **資料流目的地** 元件建立 SSIS 封裝，並將封裝部署到 SSIS 目錄。  
  
2.  執行 [SSIS 封裝發行精靈]，方法是從 C:\Program Files\Microsoft SQL Server\130\DTS\Binn 執行 ISDataFeedPublishingWizard.exe 或從 [開始] 功能表執行資料摘要發行精靈。  
  
     此精靈會使用 OLE DB Provider for SSIS (SSISOLEDB) 來建立連結的伺服器，然後建立 SQL 檢視，其中包含連結伺服器上的查詢。 此查詢包括 SSIS 目錄中的資料夾名稱、專案名稱和封裝名稱。  
  
3.  在 SQL Server Management Studio 中執行 SQL 檢視，並檢閱 SSIS 封裝的結果。 檢視會透過您建立的連結伺服器，將查詢傳送至 OLE DB Provider for SSIS。 OLE DB Provider for SSIS 會執行您在查詢中指定的封裝，然後傳回表格式結果集。  
  
> [!IMPORTANT]  
>  如需詳細步驟，請參閱 [逐步解說︰發行 SSIS 封裝作為 SQL 檢視](../../integration-services/data-flow/walkthrough-publish-an-ssis-package-as-a-sql-view.md)。  
  
## <a name="expose-output-data-from-an-ssis-package-as-an-odata-feed-by-using-the-power-bi-admin-center"></a>使用 Power BI 系統管理中心公開 SSIS 封裝的輸出資料做為 OData 摘要  
 藉由使用 Power BI 系統管理中心，IT 系統管理員可以將內部部署資料來源的資料當作 OData 摘要公開給使用者。 根據預設，Power BI 系統管理中心可讓您僅註冊 SQL Server 資料來源。 不過，您可以透過入口網站，藉由使用 **資料流目的地** 和 **Microsoft OLE DB Provider for SQL Server Integration Services (SSISOLEDB)** ，註冊 SSIS 封裝作為資料來源 ，並將 SSIS 封裝的結果資料當作 OData 摘要公開給使用者。  
  
 系統管理中心可讓您在 SQL Server 資料庫中發行檢視。 如此一來，您可以使用 SSIS 封裝發行精靈，來發行 SSIS 封裝做為 SQL 檢視。 接著，可在 Power BI 系統管理中心選取要包含於 OData 摘要中的檢視。 資料負責人可以使用適用於 Excel 的 Power Query 增益集，從 SSIS 封裝取用摘要。  
  
 如需詳細的逐步解說，請參閱 [發行 SSIS 封裝做為 OData 摘要來源](http://go.microsoft.com/fwlink/?LinkID=317367)。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [逐步解說︰發行 SSIS 封裝作為 SQL 檢視](../../integration-services/data-flow/walkthrough-publish-an-ssis-package-as-a-sql-view.md)  
  
-   [設定資料流目的地](../../integration-services/data-flow/configure-data-streaming-destination.md)  
  
## <a name="see-also"></a>請參閱＜  
 [發行 SSIS 封裝做為 OData 摘要來源](http://go.microsoft.com/fwlink/?LinkID=317367)  
  
  
