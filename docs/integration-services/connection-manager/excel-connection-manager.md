---
title: "Excel 連接管理員 |Microsoft 文件"
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.excelconnection.f1
helpviewer_keywords:
- files [Integration Services], connections
- connections [Integration Services], Excel
- Excel [Integration Services]
- connection managers [Integration Services], Excel
ms.assetid: 667419f2-74fb-4b50-b963-9197d1368cda
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2800075091835b2d6f2b07ee34e9b897fe86634e
ms.openlocfilehash: a5ce75f3c1715870113626642150028e31a0d58b
ms.contentlocale: zh-tw
ms.lasthandoff: 08/17/2017

---
# <a name="excel-connection-manager"></a>Excel 連接管理員
  Excel 連接管理員可讓封裝連接到現有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 活頁簿檔案。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含的 Excel 來源和 Excel 目的地使用 Excel 連線管理員。  
  
 當您將 Excel 連線管理員加入封裝時，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會建立一個連線管理員 (該連線管理員在執行階段會被解析為 Excel 連接)、設定連線管理員屬性，並將該連線管理員加入封裝上的 **Connections** 集合。  
  
 連線管理員的 **ConnectionManagerType** 屬性會設為 [EXCEL]。  
  
## <a name="configuration-of-the-excel-connection-manager"></a>設定 Excel 連接管理員  
 您可以利用下列方式設定 Excel 連接管理員：  
  
-   指定 Excel 活頁簿檔案的路徑。  
  
    > [!NOTE]  
    >  您不能連接到受密碼保護的 Excel 檔案。  
  
-   指定用於建立檔案的 Excel 版本。  
  
-   指出所選取工作表或範圍中第一個存取資料的資料列是否包含資料行名稱。  
  
 如果 Excel 來源使用 Excel 連接管理員，擷取的資料中便會包含資料行名稱。 如果 Excel 目的地使用 Excel 連接管理員，資料行名稱便會包含在寫入的資料中。  
  
 如需 Excel 來源和 Excel 目的地行為的詳細資訊，請參閱 [Excel 來源](../../integration-services/data-flow/excel-source.md) 和 [Excel 目的地](../../integration-services/data-flow/excel-destination.md)。  
  
 您可以透過「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 如需可在 [ [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 中設定之屬性的詳細資訊，請參閱 [Excel 連線管理員編輯器](../../integration-services/connection-manager/excel-connection-manager-editor.md)。  
  
 如需以程式設計方式設定連線管理員的資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以程式設計方式加入連線](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)。  
  
 如需循環使用 Excel 檔案群組的資訊，請參閱 [使用 Foreach 迴圈容器來循環使用 Excel 檔案和資料表](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)。  
  
## <a name="excel-connection-manager-editor"></a>Excel 連接管理員編輯器
  使用 [Excel 連線管理員編輯器] 對話方塊，將連接加入現有或新的 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 活頁簿檔案。  
  
 若要深入了解快取連線管理員，請參閱 [Excel 連線管理員](../../integration-services/connection-manager/excel-connection-manager.md)。  
  
### <a name="options"></a>選項。  
 **Excel 檔案路徑**  
 輸入現有或新的 Excel 活頁簿檔案 (.xls) 的路徑和檔案名稱。  
  
> [!NOTE]  
>  您不能連接到受密碼保護的 Excel 檔案。  
  
> [!WARNING]  
>  當您選取指向新的或非現存檔案的 [Excel 連接]，然後在 [Excel 工作表的名稱] 中按一下 [新增] 時，[Excel 目的地編輯器] 會自動建立 Excel 檔案。  
  
 **瀏覽**  
 使用 [開啟] 對話方塊導覽至 Excel 檔存在的資料夾，或您要建立新的檔案。  
  
 **Excel 版本**  
 指定用於建立檔案的 Microsoft Excel 版本。  
  
 **第一個資料列有資料行名稱**  
 指定選取之工作表中資料的第一個資料列是否包含資料行名稱。 此選項的預設值是 **[True]**。  
  
## <a name="connectivity-components-for-microsoft-excel-and-access-files"></a>Microsoft Excel 和 Access 檔案的連線元件
  
您可能要下載 Microsoft Office 檔案的連線元件，如果它們尚未安裝。 下載最新版的 Excel 和 Access 檔案的連線元件： [Microsoft Access 資料庫引擎 2016年可轉散發套件](https://www.microsoft.com/download/details.aspx?id=54920)。
  
最新版本的元件可以開啟以舊版 Excel 建立的檔案。

如果電腦有 32 位元版本的 Office，則必須安裝 32 位元版本的元件，而且您也必須確定您在 32 位元模式執行封裝。

如果您有 Office 365 訂閱，請確定您在 Access 資料庫引擎 2016年可轉散發套件並不使用 Microsoft Access 2016 執行階段時下載。 當您執行安裝程式時，您可能會看到錯誤訊息，您無法安裝下載的並存 Office 按一下來執行元件。 略過此錯誤訊息，以執行安裝以無訊息模式開啟命令提示字元視窗並執行。下載的 EXE 檔案`/quiet`切換。 例如：

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`
  
## <a name="related-tasks"></a>相關工作  
  
-   [使用 Foreach 迴圈容器來循環使用 Excel 檔案和資料表](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
-   [連接至 Excel 活頁簿](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)  
  
  

