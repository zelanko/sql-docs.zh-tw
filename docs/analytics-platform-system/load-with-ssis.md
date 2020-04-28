---
title: 使用 Integration Services 載入
description: 提供使用 SQL Server Integration Services （SSIS）套件將資料載入至平行處理資料倉儲（PDW）的參考和部署資訊。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: b0bcb5cfe1ec4111aaea7153f35bca084df62b76
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401009"
---
# <a name="load-data-with-integration-services-to-parallel-data-warehouse"></a>將具有 Integration Services 的資料載入平行處理資料倉儲
提供使用 SQL Server Integration Services （SSIS）套件將資料載入 SQL Server 平行資料倉儲的參考和部署資訊。  
  
<!-- MISSING LINKS

## <a name="BeforeBegin"></a>Before You Begin  
Before you can start loading data, use the following topics to install the Integration Services Destination Adapters and to create an Integration Services package that connects SQL Server PDW:  


-   [Install Integration Services destination adapters](install-integration-services-destination-adapters.md)  
  
-   [Connect With Integration Services for loading](connect-with-ssis-for-loading.md)  
  
For general information about developing Integration Services packages, see [Designing and Implementing Packages (Integration Services)](https://msdn.microsoft.com/library/ms141091\(v=sql11\).aspx) on MSDN.  

-->
  
## <a name="basics"></a><a name="Basics"></a>基本概念  
Integration Services 是資料的高效能解壓縮、轉換和載入（ETL）的 SQL Server 元件，通常用來填入並更新資料倉儲。  
  
PDW 目的地介面卡是一個 Integration Services 元件，可讓您使用 Integration Services .dtsx 套件，將資料載入至 PDW。 在 SQL ServerPDW 的封裝工作流程中，您可以從多個來源載入和合併資料，並將資料載入至多個目的地。 在封裝內以及同時執行的多個封裝之間，載入作業都是平行進行，同一應用裝置中最多可以有 10 個載入作業平行執行。  
  
除了本主題中所述的工作之外，您還可以使用 Integration Services 的其他功能，在將資料載入資料倉儲之前，先篩選、轉換、分析和清理您的資料。 您還可以藉由執行 SQL 陳述式、執行子封裝或傳送郵件，來加強封裝的工作流程。  
  
如需 Integration Services 的完整檔，請參閱[SQL Server Integration Services](../integration-services/sql-server-integration-services.md)。  
  
## <a name="methods-for-running-an-integration-services-package"></a><a name="HowToDeployPackage"></a>執行 Integration Services 封裝的方法  
使用其中一種方法來執行 Integration Services 套件。  
  
### <a name="run-from-sql-server-2008-r2-business-intelligence-development-studio-bids"></a>從 SQL Server 2008 R2 Business Intelligence Development Studio （投標）執行  
若要從出價內執行封裝，請以滑鼠右鍵按一下您的套件，然後選擇 [**執行封裝**]。  
  
根據預設，投標會執行使用64位二進位檔的套件。 這是由**Run64BitRuntime** package 屬性所決定。 若要設定此屬性，請移至**方案總管**，以滑鼠右鍵按一下您的專案，然後選擇 [**屬性**]。 在**Integration Services] 屬性頁**上，移至 [設定] [**屬性**]，然後選取 [**調試**]。 您會在 [**調試選項**] 底下看到**Run64BitRuntime**屬性。 若要使用32位執行時間，請將此設定為**False**。 若要使用64位執行時間，請將此設定為**True**。  
  
### <a name="run-from-sql-server-2012-sql-server-data-tools"></a>從 SQL Server 2012 SQL Server Data Tools 執行  
若要從 SQL Server Data Tools 內執行封裝，請以滑鼠右鍵按一下您的封裝，然後選擇 [**執行封裝**]。  
  
### <a name="run-from-powershell"></a>從 PowerShell 執行  
若要從 Windows PowerShell 執行封裝，請使用**dtexec**公用程式：`dtexec /FILE <packagePath>`  
  
例如， `dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`  
  
### <a name="run-from-a-windows-command-prompt"></a>從 Windows 命令提示字元執行 
若要從 Windows 命令提示字元執行封裝，請使用**dtexec**公用程式：`dtexec /FILE <packagePath>`  
  
例如： `dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`  
  
## <a name="data-types"></a><a name="DataTypes"></a>資料類型  
當您使用 Integration Services 將資料從資料來源載入 SQL Server PDW 資料庫時，資料會先從來源資料對應到 Integration Services 的資料類型。 這樣可以讓多個資料來源的資料對應至共同的一組資料類型。  
  
然後，資料會從 Integration Services 對應到 SQL Server PDW 的資料類型。 針對每個 SQL Server PDW 資料類型，下表列出可以轉換成 SQL Server PDW 資料類型的 Integration Services 資料類型。  
  
|PDW 資料類型|對應至 PDW 資料類型 Integration Services 資料類型|  
|---------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|  
|BIT|DT_BOOL|  
|bigint|DT_I1、DT_I2、DT_I4、DT_I8、DT_UI1、DT_UI2、DT_UI4|  
|CHAR|DT_STR|  
|日期|DT_DBDATE|  
|DATETIME|DT_DATE、DT_DBDATE、DT_DBTIMESTAMP、DT_DBTIMESTAMP2|  
|DATETIME2|DT_DATE、DT_DBDATE、DT_DBTIMESTAMP、DT_DBTIMESTAMP2|  
|DATETIMEOFFSET|DT_WSTR|  
|DECIMAL|DT_DECIMAL、DT_I1、DT_I2、DT_I4、DT_I4、DT_I8、DT_NUMERIC、DT_UI1、DT_UI2、DT_UI4、DT_UI8|  
|FLOAT|DT_R4、DT_R8|  
|INT|DT_I1、DTI2、DT_I4、DT_UI1、DT_UI2|  
|MONEY|DT_CY|  
|NCHAR|DT_WSTR|  
|NUMERIC|DT_DECIMAL、DT_I1、DT_I2、DT_I4、DT_I8、DT_NUMERIC、DT_UI1、DT_UI2、DT_UI4、DT_UI8|  
|NVARCHAR|DT_WSTR、DT_STR|  
|real|DT_R4|  
|SMALLDATETIME|DT_DBTIMESTAMP2|  
|SMALLINT|DT_I1、DT_I2、DT_UI1|  
|SMALLMONEY|DT_R4|  
|TIME|DT_WSTR|  
|TINYINT|DT_I1|  
|VARBINARY|DT_BYTES|  
|VARCHAR|DT_STR|  
  
**資料類型精確度的有限支援**  
  
如果您對應的 DT_NUMERIC 或 DT_DECIMAL 輸入資料行中包含有效位數大於28的值，則 PDW 會產生驗證錯誤。  
  
**不支援的資料類型**  
  
SQL Server PDW 不支援下列 Integration Services 的資料類型：  
  
-   DT_DBTIMESTAMPOFFSET  
  
-   DT_DBTIME2  
  
-   DT_GUID  
  
-   DT_IMAGE  
  
-   DT_NTEXT  
  
-   DT_TEXT  
  
若要將包含這些類型資料的資料行載入 SQL Server PDW 中，您必須在資料流程中加入「資料轉換」轉換，將資料轉換成相容的資料類型。  
  
## <a name="permissions"></a>權限  
若要執行 Integration Services 載入封裝，您需要：  
  
-   資料庫的載入許可權。  
  
-   適用于目的地資料表的插入、更新、刪除許可權。  
  
-   如果使用了臨時資料庫，就會在臨時資料庫上建立許可權。 這是用來建立臨時表。  
  
-   如果沒有使用任何臨時資料庫，請在目的地資料庫上建立許可權。 這是用來建立臨時表。  
  
## <a name="general-remarks"></a><a name="GenRemarks"></a>一般備註  
當 Integration Services 封裝有多個 SQL Server PDW 目的地執行，而其中一個連接已終止時，Integration Services 會停止將資料推送至所有 SQL Server PDW 目的地。  
  
## <a name="limitations-and-restrictions"></a><a name="Limits"></a>限制事項  
若為 Integration Services 封裝，相同資料來源的 SQL Server PDW 目的地數目會受限於作用中負載的最大數目。 上限是預先設定的，使用者無法設定。 

<!-- MISSING LINKS
For the maximum number of loads and queued loads per appliance, see [Minimum and maximum values](minimum-and-maximum-values.md).  
-->
  
相同資料來源的每個 Integration Services 封裝目的地都會計為執行封裝時的一個負載。 例如，假設使用中載入數目上限為 10。 如果封裝嘗試針對相同的資料來源開啟 11 個以上的目的地，則封裝不會執行。  
  
只要封裝使用的使用中載入數目不要超過上限，就可以同時執行多個封裝。 例如，若使用中載入數目上限為 10，您就可以同時執行兩個各使用 10 個目的地的封裝。 當一個封裝執行時，另一個封裝就會在載入佇列中等待。  
  
如果載入佇列中的佇列數目超過佇列的載入數目上限，封裝就不會執行。 例如，如果每個設備的載入數目上限為10，而佇列的載入數目上限為每個設備40，則您可以同時執行五個每個開啟10個目的地的 Integration Services 套件。 如果您嘗試執行第六個封裝，就不會執行。  

> [!IMPORTANT]
> 當來源資料表包含具有 SQL 定序的 char 和 Varchar 資料行時，使用 SSIS 中的 OLE DB 資料來源搭配 PDW 目的地介面卡，可能會導致資料損毀。 如果來源資料表包含具有 SQL 定序的 char 或 Varchar 資料行，我們建議使用 ADO.NET 的來源。 

  
## <a name="locking-behavior"></a><a name="Locks"></a>鎖定行為  
使用 Integration Services 載入資料時，SQL ServerPDW 會使用資料列層級鎖定來更新目的地資料表中的資料。 這表示在更新每個資料列時，都會鎖定其讀取和寫入功能。 將資料載入暫存資料表時，並不會鎖定目的地資料表中的資料列。  
  
## <a name="examples"></a><a name="Examples"></a>範例  
  
### <a name="a-simple-load-from-flat-file"></a><a name="Walkthrough"></a>A. 一般檔案中的簡單載入  
下列逐步解說示範使用 Integration Services 將一般檔案資料載入 SQL Server PDW 設備的簡單資料載入。  這個範例假設已在用戶端電腦上安裝 Integration Services，而且已安裝 SQL Server PDW 目的地，如上所述。  
  
在此範例中，我們將載入`Orders`具有下列 DDL 的資料表。 `Orders`資料表是`LoadExampleDB`資料庫的一部分。  
  
```sql  
CREATE TABLE LoadExampleDB.dbo.Orders (  
   id INT,  
   city varchar(25),  
   lastUpdateDate DATE,  
   orderDate DATE)  
;  
```  
  
以下是載入資料：  
  
```  
id        city           lastUpdateDate     orderdate  
--------- -------------- ------------------ ----------  
1         Seattle        2010-05-01         2010-01-01  
2         Denver         2002-06-25         1999-01-02  
```  
  
在準備載入時，請建立`exampleLoad.txt`包含載入資料的一般檔案：  
  
```  
id,city,lastUpdateDate,orderDate  
1,Seattle,2010-05-01,2010-01-01  
2,Denver,2002-06-25,1999-01-02  
```  
  
首先，執行下列步驟來建立 Integration Services 封裝：  
  
1.  在 SQL Server Data Tools \(SSDT\)中，**選取 [** 檔案]、[**新增**] 和 [**專案**]。 從列出的選項中選取 [ **Integration Services 專案**]。 為此專案`ExampleLoad`命名，然後按一下 **[確定]**。  
  
2.  按一下 [**控制流程**] 索引標籤，然後將 [**資料流程**工作] 從 [**工具箱**] 拖曳至 [**控制流程**] 窗格。  
  
3.  按一下 [**資料流程] 索引**標籤，然後從 [**工具箱**] 將 [一般檔案**來源**] 拖曳至 [**資料流程**] 窗格。 按兩下您剛才建立的方塊，以開啟 [一般檔案**來源編輯器**]。  
  
4.  按一下 [**連接管理員**]，然後按一下 [**新增**]。  
  
5.  在 [**連接管理員名稱**] 方塊中，輸入連接的易記名稱。 在此範例中`Example Load Flat File CM`為。  
  
6.  按一下 **[流覽]** ， `ExampleLoad.txt`然後從本機電腦選取檔案。  
  
7.  因為一般檔案包含具有資料行名稱的資料列，請按一下**第一個資料列方塊中的資料行名稱**。  
  
8.  按一下左欄中的 [資料**行**]，並預覽將要載入的資料，以確保正確地解讀資料行名稱和資料。  
  
9. 按一下左側資料行中的 [ **Advanced** ]。 按一下每個資料行名稱，以檢查與資料相關聯的資料類型。 在方塊中輸入變更，讓載入之資料的資料類型與目的地資料行類型相容。  
  
10. 按一下 **[確定]** 儲存您的連線管理員。  
  
11. 按一下 **[確定]** 以結束 [一般檔案**來源編輯器**]。  
  
指定資料流程的目的地。  
  
1.  將 [ **SQL Server PDW 目的地**從 [**工具箱**] 拖曳至 [**資料流程**] 窗格。  
  
2.  按兩下您剛才建立的方塊，以載入 [ **SQL Server PDW 目的地編輯器**]。  
  
3.  按一下 [**連接管理員**] 旁的向下箭號。  
  
4.  選取 [**建立新的連接**]。  
  
5.  在 [伺服器]、[使用者]、[密碼] 和 [目的地] 資料庫中填入您應用裝置特定資訊的資訊。 （範例如下所示）。 然後按一下 [ **確定**]。  
  
    針對 [未連接的連線]，**伺服器名稱**：輸入 <設備名稱>-SQLCTL01，17001。  
  
    針對 [乙太網路連線]，[**伺服器名稱**]：輸入控制節點叢集的 IP 位址，逗號，埠17001。 例如，10.192.63.134、17001。  
  
    **使用者**`user1`  
  
    **許可權**`password1`  
  
    **目的地資料庫：**`LoadExampleDB`  
  
6.  選取目的地資料表： `Orders`。  
  
7.  選取 [**附加**] 做為載入模式，然後按一下 **[確定]**。  
  
指定從來源到目的地的資料流程。  
  
1.  在 [**資料流程**] 窗格中，將綠色箭號從 [一般檔案**來源**] 方塊拖曳到 [ **SQL Server PDW 目的地**] 方塊中。  
  
2.  按兩下 [ **SQL Server PDW 目的地**] 方塊，讓您再次看到 [ **SQL Server PDW 目的地編輯器**]。 在 [未對應的**輸入資料行**] 底下，您應該會看到位於左側一般檔案的資料行名稱。 您應該會在 [未對應的**目的地資料行**] 底下的右邊，看到目的地資料表的資料行名稱。 在對應的 [**輸入資料行**] 和 [未**對應**的**目的地資料行**] 清單中，拖曳或按兩下相符的資料行名稱，以對應資料行。 按一下 [確定] **** 儲存設定。  
  
3.  按一下 [檔案] 功能表中的 [**儲存** **]，以**儲存封裝。  
  
在您的電腦上執行封裝 Integration Services。  
  
1.  在 [Integration Services**方案總管**（右欄）中，以滑鼠右鍵`Package.dtsx`按一下並選取 [**執行**]。  
  
2.  封裝將會執行，並在**進度**窗格上顯示進度加上任何錯誤。 使用 SQL 用戶端來確認負載，或透過 SQL Server PDW 管理主控台來監視負載。  
  
## <a name="see-also"></a>另請參閱  
[建立使用 SSIS PDW 目的地介面卡的腳本工作](create-ssis-script-task-using-pdw-destination-adapter.md)  
[SQL Server Integration Services](../integration-services/sql-server-integration-services.md)  
[設計和實作封裝 (Integration Services)](https://msdn.microsoft.com/library/ms141091\(v=sql11\).aspx)  
[教學課程：使用精靈建立基本封裝](https://technet.microsoft.com/library/ms365330\(v=sql11\).aspx)  
[消費者入門（Integration Services）](https://go.microsoft.com/fwlink/?LinkId=202412)  
[動態套件產生範例](https://go.microsoft.com/fwlink/?LinkId=202413)  
[設計平行處理原則的 SSIS 封裝 (SQL Server 視訊)](https://msdn.microsoft.com/library/dd795221.aspx)  
[Microsoft SQL Server 的社區範例： Integration Services](https://go.microsoft.com/fwlink/?LinkId=202415)  
[利用異動資料擷取改善累加式載入](../integration-services/change-data-capture/change-data-capture-ssis.md)  
[緩時變維度轉換](../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)  
[大量插入工作](../integration-services/control-flow/bulk-insert-task.md)  
  
<!-- MISSING LINKS
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examples](metadata-query-examples.md)
-->
