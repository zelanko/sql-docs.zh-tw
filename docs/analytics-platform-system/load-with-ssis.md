---
title: 使用 Integration Services-平行處理資料倉儲載入 |Microsoft Docs
description: 提供用於載入資料到 Parallel Data Warehouse (PDW) 使用 SQL Server Integration Services (SSIS) 套件的參考和部署資訊。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: b8a1ca0ec3662dddb2baa5fbac5fe01ed4d4f2e5
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51700909"
---
# <a name="load-data-with-integration-services-to-parallel-data-warehouse"></a>使用平行處理資料倉儲的 Integration Services 載入資料
提供使用 SQL Server Integration Services (SSIS) 封裝將資料載入 SQL Server Parallel Data Warehouse 的參考和部署資訊。  
  
<!-- MISSING LINKS

## <a name="BeforeBegin"></a>Before You Begin  
Before you can start loading data, use the following topics to install the Integration Services Destination Adapters and to create an Integration Services package that connects SQL Server PDW:  


-   [Install Integration Services destination adapters](install-integration-services-destination-adapters.md)  
  
-   [Connect With Integration Services for loading](connect-with-ssis-for-loading.md)  
  
For general information about developing Integration Services packages, see [Designing and Implementing Packages (Integration Services)](https://msdn.microsoft.com/library/ms141091\(v=sql11\).aspx) on MSDN.  

-->
  
## <a name="Basics"></a>基本概念  
Integration Services 是高效能擷取、 轉換和載入 (ETL) 的資料，SQL Server 元件，和通常用來填入，並更新資料倉儲。  
  
PDW 目的地配接器是可讓您使用 Integration Services dtsx 封裝將資料載入 PDW 的 Integration Services 元件。 在 SQL ServerPDW 封裝工作流程，您可以載入，並合併多個來源的資料，以及將資料載入至多個目的地。 在封裝內以及同時執行的多個封裝之間，載入作業都是平行進行，同一應用裝置中最多可以有 10 個載入作業平行執行。  
  
除了本主題中所述的工作，您可以使用 Integration Services 的其他功能來篩選、 轉換、 分析並清理之前將資料載入資料倉儲的資料。 您還可以藉由執行 SQL 陳述式、執行子封裝或傳送郵件，來加強封裝的工作流程。  
  
Integration services 的完整文件，請參閱 < [SQL Server Integration Services](../integration-services/sql-server-integration-services.md)。  
  
## <a name="HowToDeployPackage"></a>執行 Integration Services 封裝的方法  
您可以使用其中一種方法來執行 Integration Services 封裝。  
  
### <a name="run-from-sql-server-2008-r2-business-intelligence-development-studio-bids"></a>從 SQL Server 2008 R2 Business Intelligence Development Studio (BIDS 中) 執行  
若要執行中的套件在 BIDS 內，以滑鼠右鍵按一下您的套件，然後選擇**執行封裝**。  
  
根據預設，BIDS 會執行使用 64 位元二進位檔案的套件。 這取決於**Run64BitRuntime**封裝屬性。 若要設定這個屬性，請前往**方案總管**，以滑鼠右鍵按一下您的專案，然後選擇**屬性**。 在  **Integration Services 屬性頁**，請移至**組態屬性**，然後選取**偵錯**。 您會看到**Run64BitRuntime**下方的屬性**偵錯選項**。 若要使用 32 位元執行階段，將此設**False**。 若要使用 64 位元執行階段，將此設 **，則為 True**。  
  
### <a name="run-from-sql-server-2012-sql-server-data-tools"></a>執行從 SQL Server 2012 的 SQL Server 資料工具  
若要執行封裝的 SQL Server Data Tools 中，以滑鼠右鍵按一下您的套件，然後選擇**執行封裝**。  
  
### <a name="run-from-powershell"></a>從 PowerShell 執行  
若要執行封裝，從 Windows PowerShell，使用**dtexec**公用程式： `dtexec /FILE <packagePath>`  
  
例如： `dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`   
  
### <a name="run-from-a-windows-command-prompt"></a>執行從 Windows 命令提示字元 
若要執行封裝，從 Windows 命令提示字元中，使用**dtexec**公用程式： `dtexec /FILE <packagePath>`  
  
例如： `dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`  
  
## <a name="DataTypes"></a>資料類型  
當使用 Integration Services 資料來源的資料載入到 SQL Server PDW 資料庫時，資料會第一次從來源資料對應至 Integration Services 資料類型。 這樣可以讓多個資料來源的資料對應至共同的一組資料類型。  
  
然後資料會從 Integration Services 對應至 SQL Server PDW 資料型別。 每個 SQL Server PDW 資料類型下, 表列出可以轉換成 SQL Server PDW 資料類型的 Integration Services 資料類型。  
  
|PDW 資料類型|Integration Services 資料類型 (s) 對應至 PDW 資料型別|  
|---------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|  
|BIT|DT_BOOL|  
|bigint|DT_I1、DT_I2、DT_I4、DT_I8、DT_UI1、DT_UI2、DT_UI4|  
|CHAR|DT_STR|  
|DATE|DT_DBDATE|  
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
  
**針對資料類型有效位數的有限的支援**  
  
PDW 會產生驗證錯誤，如果您將對應的 DT_NUMERIC 或 DT_DECIMAL 輸入資料行包含有效位數大於 28 的值。  
  
**不支援的資料類型**  
  
SQL Server PDW 不支援下列的 Integration Services 資料類型：  
  
-   DT_DBTIMESTAMPOFFSET  
  
-   DT_DBTIME2  
  
-   DT_GUID  
  
-   DT_IMAGE  
  
-   DT_NTEXT  
  
-   DT_TEXT  
  
若要載入到 SQL Server PDW 中包含這些資料類型的資料行，您必須將資料轉換成相容的資料類型的資料流程中新增上游資料轉換 」。  
  
## <a name="permissions"></a>Permissions  
若要執行的 Integration Services 載入封裝，您需要：  
  
-   載入資料庫的權限。  
  
-   適用於 INSERT、 UPDATE 目的地資料表上的刪除權限。  
  
-   如果使用暫存資料庫時，建立暫存資料庫的權限。 這是建立暫存資料表。  
  
-   如果不使用任何暫存資料庫時，目的地資料庫上的建立權限。 這是建立暫存資料表。  
  
## <a name="GenRemarks"></a>一般備註  
當 Integration Services 封裝執行的多個 SQL Server PDW 目的地，且其中一個連線終止時，Integration Services 就會停止將資料推送到所有的 SQL Server PDW 目的地。  
  
## <a name="Limits"></a>限制事項  
Integration Services 封裝，相同的資料來源的 SQL Server PDW 目的地數目受限於使用中載入數目上限。 上限是預先設定的，使用者無法設定。 

<!-- MISSING LINKS
For the maximum number of loads and queued loads per appliance, see [Minimum and maximum values](minimum-and-maximum-values.md).  
-->
  
相同的資料來源的每個 Integration Services 封裝目的地計為一個載入時執行封裝。 例如，假設使用中載入數目上限為 10。 如果封裝嘗試針對相同的資料來源開啟 11 個以上的目的地，則封裝不會執行。  
  
只要封裝使用的使用中載入數目不要超過上限，就可以同時執行多個封裝。 例如，若使用中載入數目上限為 10，您就可以同時執行兩個各使用 10 個目的地的封裝。 當一個封裝執行時，另一個封裝就會在載入佇列中等待。  
  
如果載入佇列中的佇列數目超過佇列的載入數目上限，封裝就不會執行。 例如，如果載入的最大數目是每一設備 10 的已排入佇列的載入數目上限為每一設備的 40，您可以同時執行五個的 Integration Services 封裝，各開啟 10 個目的地。 如果您嘗試執行第六個封裝，就不會執行。  

> [!IMPORTANT]
> 在 SSIS 的 OLE DB 資料來源使用 PDW 目的地配接器，可能會導致資料損毀，如果來源資料表包含具有 SQL 定序的 char 和 varchar 資料行。 我們建議使用 ADO.NET 來源，如果來源資料表包含具有 SQL 定序的 char 或 varchar 資料行。 

  
## <a name="Locks"></a>鎖定行為  
載入與 Integration Services 資料時，SQL ServerPDW 會使用資料列層級鎖定來更新目的地資料表中的資料。 這表示在更新每個資料列時，都會鎖定其讀取和寫入功能。 將資料載入暫存資料表時，並不會鎖定目的地資料表中的資料列。  
  
## <a name="Examples"></a>範例  
  
### <a name="Walkthrough"></a>A。 簡單的負載，從一般檔案  
下列逐步解說會示範簡單的資料負載，使用 載入至 SQL Server PDW 應用裝置的一般檔案資料 Integration Services。  這個範例將假設用戶端機器上的 Integration Services 已經安裝，而且已安裝 SQL Server PDW 目的地，如上面所述。  
  
在此範例中，我們會載入到`Orders`有下列 DDL 的資料表。 `Orders`資料表會是一部分`LoadExampleDB`資料庫。  
  
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
  
在負載的準備工作，會建立一般檔案`exampleLoad.txt`，包含載入資料：  
  
```  
id,city,lastUpdateDate,orderDate  
1,Seattle,2010-05-01,2010-01-01  
2,Denver,2002-06-25,1999-01-02  
```  
  
首先，建立 Integration Services 封裝，執行下列步驟：  
  
1.  在 SQL Server Data Tools \(SSDT\)，選取**檔案**，**新增**，然後**專案**。 選取  **Integration Services 專案**從所列的選項。 此專案的名稱， `ExampleLoad`，然後按一下 **[確定]**。  
  
2.  按一下 **控制流程**索引標籤，然後將**Data Flow Task**從**工具箱**至**控制流程**窗格。  
  
3.  按一下 **資料流程**索引標籤，然後將**一般檔案來源**從**工具箱**至**資料流程**窗格。 連按兩下您剛才建立開啟的方塊**一般檔案來源編輯器**。  
  
4.  按一下 **連接管理員**，然後按一下**新增**。  
  
5.  在 **連接管理員名稱**方塊中，輸入連接的易記名稱。 此範例中，針對`Example Load Flat File CM`。  
  
6.  按一下 **瀏覽**，然後選取`ExampleLoad.txt`檔案從本機電腦。  
  
7.  由於一般檔案包含具有資料行名稱的資料列，按一下**第一個資料列中的資料行名稱** 方塊中。  
  
8.  按一下 **資料行**左欄中，與預覽會載入以確定資料行名稱的資料和資料已正確解譯。  
  
9. 按一下 **進階**左側資料行中。 按一下每個資料行名稱，以檢閱已與資料相關聯的資料類型。 以便載入資料的資料類型將會與目的地資料行類型相容，則請在方塊中輸入變更。  
  
10. 按一下 **確定**以儲存您的連接管理員。  
  
11. 按一下  **確定**以結束**一般檔案來源編輯器**。  
  
指定資料流程的目的地。  
  
1.  拖曳**SQL Server PDW 目的地**從**工具箱**來**資料流程**窗格。  
  
2.  按兩下您剛才用來載入方塊**SQL Server PDW 目的地編輯器**。  
  
3.  按一下向下箭號旁**連接管理員**。  
  
4.  選取 **建立新的連接**。  
  
5.  填寫您的應用裝置的特定資訊的伺服器、 使用者、 密碼和目的地資料庫的資訊。 （範例如下所示）。 然後按一下 [確定]。  
  
    InfiniBand 連線**伺服器名稱**： 輸入 < 設備名稱 >-SQLCTL01，接著 17001。  
  
    為乙太網路連線**伺服器名稱**： 輸入的控制節點的叢集、 逗點和連接埠接著 17001 的 IP 位址。 比方說，10.192.63.134,17001。  
  
    **使用者：**`user1`  
  
    **密碼：**`password1`  
  
    **目的地資料庫：**`LoadExampleDB`  
  
6.  選取目的地資料表： `Orders`。  
  
7.  選取  **Append**作為載入模式，然後按一下**確定**。  
  
指定資料流的來源到目的地。  
  
1.  在上**資料流程**窗格中，將從綠色箭頭拖曳**一般檔案來源**方塊**SQL Server PDW 目的地** 方塊中。  
  
2.  按兩下**SQL Server PDW 目的地**方塊，讓您看到**SQL Server PDW 目的地編輯器**一次。 您應該會下看到資料行名稱，從一般檔案，在左側**未對應的輸入資料行**。 您應該會看到目的地資料表的資料行名稱在右側，底下**未對應的目的地資料行**。 拖曳或按兩下相符的資料行中對應的資料行**未對應的輸入資料行**並**未對應的目的地資料行**若要列出**對應的資料行**方塊。 按一下 **確定**以儲存設定。  
  
3.  按一下 儲存封裝**儲存**中**檔案**功能表。  
  
在 Integration Services 的電腦上執行封裝。  
  
1.  在 Integration Services**方案總管**（右欄），以滑鼠右鍵按一下`Package.dtsx`，然後選取**Execute**。  
  
2.  封裝執行和上，則會顯示進度，以及任何錯誤**進度**窗格。 若要確認負載，使用 SQL 用戶端，或監視 SQL Server PDW 管理主控台透過負載。  
  
## <a name="see-also"></a>另請參閱  
[建立指令碼工作使用 SSIS PDW 目的地配接器](create-ssis-script-task-using-pdw-destination-adapter.md)  
[SQL Server Integration Services](../integration-services/sql-server-integration-services.md)  
[設計和實作封裝 (Integration Services)](https://msdn.microsoft.com/library/ms141091\(v=sql11\).aspx)  
[教學課程： 建立基本封裝，使用精靈](https://technet.microsoft.com/library/ms365330\(v=sql11\).aspx)  
[開始使用 (Integration Services)](https://go.microsoft.com/fwlink/?LinkId=202412)  
[動態封裝產生範例](https://go.microsoft.com/fwlink/?LinkId=202413)  
[設計您的 SSIS 套件的平行處理原則 （SQL Server 影片）](https://msdn.microsoft.com/library/dd795221.aspx)  
[Microsoft SQL Server 社群範例： Integration Services](https://go.microsoft.com/fwlink/?LinkId=202415)  
[與異動資料擷取改善累加式載入](../integration-services/change-data-capture/change-data-capture-ssis.md)  
[緩時變維度轉換](../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)  
[大量插入工作](../integration-services/control-flow/bulk-insert-task.md)  
  
<!-- MISSING LINKS
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examples](metadata-query-examples.md)
-->
