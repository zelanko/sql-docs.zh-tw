---
title: 使用 Integration Services 載入
description: 提供使用 SQL Server Integration Services (SSIS) 封裝將資料載入平行資料倉儲 (PDW) 的參考和部署資訊。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ea2a4f39b16fe2f8b23d6a6a229ce9b936e6e6d7
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88766757"
---
# <a name="load-data-with-integration-services-to-parallel-data-warehouse"></a>使用 Integration Services 將資料載入平行處理資料倉儲
提供使用 SQL Server Integration Services (SSIS) 套件將資料載入 SQL Server 平行資料倉儲的參考和部署資訊。  
  
<!-- MISSING LINKS

## <a name="BeforeBegin"></a>Before You Begin  
Before you can start loading data, use the following topics to install the Integration Services Destination Adapters and to create an Integration Services package that connects SQL Server PDW:  


-   [Install Integration Services destination adapters](install-integration-services-destination-adapters.md)  
  
-   [Connect With Integration Services for loading](connect-with-ssis-for-loading.md)  
  
For general information about developing Integration Services packages, see [Designing and Implementing Packages (Integration Services)](https://msdn.microsoft.com/library/ms141091\(v=sql11\).aspx) on MSDN.  

-->
  
## <a name="basics"></a><a name="Basics"></a>基本概念  
Integration Services 是 SQL Server 的元件，可進行高效能的解壓縮、轉換和載入 (ETL 的資料) ，通常用來填入和更新資料倉儲。  
  
PDW 目的地介面卡是一種 Integration Services 元件，可讓您使用 Integration Services .dtsx 套件將資料載入 PDW。 在 SQL ServerPDW 的封裝工作流程中，您可以從多個來源載入和合併資料，並將資料載入至多個目的地。 在封裝內以及同時執行的多個封裝之間，載入作業都是平行進行，同一應用裝置中最多可以有 10 個載入作業平行執行。  
  
除了本主題中所述的工作之外，您還可以使用 Integration Services 的其他功能來篩選、轉換、分析和清理資料，然後再將資料載入資料倉儲。 您還可以藉由執行 SQL 陳述式、執行子封裝或傳送郵件，來加強封裝的工作流程。  
  
如需 Integration Services 的完整檔，請參閱 [SQL Server Integration Services](../integration-services/sql-server-integration-services.md)。  
  
## <a name="methods-for-running-an-integration-services-package"></a><a name="HowToDeployPackage"></a>執行 Integration Services 套件的方法  
使用其中一種方法來執行 Integration Services 套件。  
  
### <a name="run-from-sql-server-2008-r2-business-intelligence-development-studio-bids"></a>從 SQL Server 2008 R2 Business Intelligence Development Studio (投標)   
若要從投標內執行封裝，請以滑鼠右鍵按一下您的封裝，然後選擇 [ **執行封裝**]。  
  
根據預設，投標會使用64位的二進位檔來執行封裝。 這是由 **Run64BitRuntime** package 屬性所決定。 若要設定此屬性，請移至 **方案總管**，以滑鼠右鍵按一下您的專案，然後選擇 [ **屬性**]。 在 [ **Integration Services] 屬性頁**上，移至 [設定 **屬性** ]，然後選取 [ **調試**]。 您將會在**Debug 選項**底下看到**Run64BitRuntime**屬性。 若要使用32位執行時間，請將此設定為 **False**。 若要使用64位執行時間，請將此設定為 **True**。  
  
### <a name="run-from-sql-server-2012-sql-server-data-tools"></a>從 SQL Server 2012 SQL Server Data Tools 執行  
若要從 SQL Server Data Tools 內執行封裝，請以滑鼠右鍵按一下您的封裝，然後選擇 [ **執行封裝**]。  
  
### <a name="run-from-powershell"></a>從 PowerShell 執行  
若要從 Windows PowerShell 執行封裝，請使用 **dtexec** 公用程式： `dtexec /FILE <packagePath>`  
  
例如， `dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`  
  
### <a name="run-from-a-windows-command-prompt"></a>從 Windows 命令提示字元執行 
若要使用 **dtexec** 公用程式，從 Windows 命令提示字元執行封裝： `dtexec /FILE <packagePath>`  
  
例如：`dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`  
  
## <a name="data-types"></a><a name="DataTypes"></a>資料類型  
使用 Integration Services 將資料從資料來源載入至 SQL Server PDW 資料庫時，資料會先從來源資料對應到 Integration Services 資料類型。 這樣可以讓多個資料來源的資料對應至共同的一組資料類型。  
  
然後，資料會從 Integration Services 對應到 SQL Server PDW 資料類型。 針對每個 SQL Server PDW 資料類型，下表列出可以轉換成 SQL Server PDW 資料類型的 Integration Services 資料類型。  
  
|PDW 資料類型|Integration Services 資料類型 (s 對應到 PDW 資料類型的) |  
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
|REAL|DT_R4|  
|SMALLDATETIME|DT_DBTIMESTAMP2|  
|SMALLINT|DT_I1、DT_I2、DT_UI1|  
|SMALLMONEY|DT_R4|  
|TIME|DT_WSTR|  
|TINYINT|DT_I1|  
|VARBINARY|DT_BYTES|  
|VARCHAR|DT_STR|  
  
**有限的資料類型精確度支援**  
  
如果您對應的 DT_NUMERIC 或 DT_DECIMAL 的輸入資料行包含有效位數大於28的值，則 PDW 會產生驗證錯誤。  
  
**不支援的資料類型**  
  
SQL Server PDW 不支援下列 Integration Services 資料類型：  
  
-   DT_DBTIMESTAMPOFFSET  
  
-   DT_DBTIME2  
  
-   DT_GUID  
  
-   DT_IMAGE  
  
-   DT_NTEXT  
  
-   DT_TEXT  
  
若要將包含這些類型資料的資料行載入 SQL Server PDW 中，您必須在資料流程中加入上游的資料轉換，以將資料轉換成相容的資料類型。  
  
## <a name="permissions"></a>權限  
若要執行 Integration Services 載入封裝，您需要：  
  
-   資料庫的 LOAD 許可權。  
  
-   適用于目的地資料表的 INSERT、UPDATE、DELETE 許可權。  
  
-   如果使用臨時資料庫，請建立臨時資料庫的許可權。 這是用來建立臨時表。  
  
-   如果未使用任何臨時資料庫，請在目的地資料庫上建立許可權。 這是用來建立臨時表。  
  
## <a name="general-remarks"></a><a name="GenRemarks"></a>一般備註  
當 Integration Services 套件有多個 SQL Server PDW 目的地正在執行，且其中一個連線終止時，Integration Services 會停止將資料推送至所有 SQL Server PDW 目的地。  
  
## <a name="limitations-and-restrictions"></a><a name="Limits"></a>限制  
若為 Integration Services 封裝，相同資料來源的 SQL Server PDW 目的地數目會受限於作用中載入的數目上限。 上限是預先設定的，使用者無法設定。 

<!-- MISSING LINKS
For the maximum number of loads and queued loads per appliance, see [Minimum and maximum values](minimum-and-maximum-values.md).  
-->
  
當封裝正在執行時，相同資料來源的每個 Integration Services 封裝目的地都會計算為一個負載。 例如，假設使用中載入數目上限為 10。 如果封裝嘗試針對相同的資料來源開啟 11 個以上的目的地，則封裝不會執行。  
  
只要封裝使用的使用中載入數目不要超過上限，就可以同時執行多個封裝。 例如，若使用中載入數目上限為 10，您就可以同時執行兩個各使用 10 個目的地的封裝。 當一個封裝執行時，另一個封裝就會在載入佇列中等待。  
  
如果載入佇列中的佇列數目超過佇列的載入數目上限，封裝就不會執行。 例如，如果每個設備的負載上限為10，且佇列的載入數目上限為每個設備40，則您可以同時執行五個 Integration Services 套件，每個都開啟10個目的地。 如果您嘗試執行第六個封裝，就不會執行。  

> [!IMPORTANT]
> 當來源資料表包含具有 SQL 定序的 char 和 Varchar 資料行時，使用 SSIS 的 OLE DB 資料來源搭配 PDW 目的地介面卡，可能會導致資料損毀。 如果來源資料表包含具有 SQL 定序的 char 或 Varchar 資料行，我們建議使用 ADO.NET 來源。 

  
## <a name="locking-behavior"></a><a name="Locks"></a>鎖定行為  
使用 Integration Services 載入資料時，SQL ServerPDW 會使用資料列層級鎖定來更新目的地資料表中的資料。 這表示在更新每個資料列時，都會鎖定其讀取和寫入功能。 將資料載入暫存資料表時，並不會鎖定目的地資料表中的資料列。  
  
## <a name="examples"></a><a name="Examples"></a>範例  
  
### <a name="a-simple-load-from-flat-file"></a><a name="Walkthrough"></a>A. 從一般檔案簡單載入  
下列逐步解說示範使用 Integration Services 將一般檔案資料載入 SQL Server PDW 設備的簡單資料載入。  此範例假設 Integration Services 已安裝在用戶端電腦上，並已安裝 SQL Server PDW 目的地（如上所述）。  
  
在此範例中，我們將載入 `Orders` 具有下列 DDL 的資料表。 `Orders`資料表是資料庫的一部分 `LoadExampleDB` 。  
  
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
  
在準備載入時，請建立 `exampleLoad.txt` 包含載入資料的一般檔案：  
  
```  
id,city,lastUpdateDate,orderDate  
1,Seattle,2010-05-01,2010-01-01  
2,Denver,2002-06-25,1999-01-02  
```  
  
首先，執行下列步驟來建立 Integration Services 套件：  
  
1.  在 SQL Server Data Tools \( SSDT 中 \) ， **File**選取 [檔案]、[**新增**] 和 [**專案**]。 從列出的選項中選取 [ **Integration Services 專案** ]。 將此專案命名為 `ExampleLoad` ，然後按一下 **[確定]**。  
  
2.  按一下 [ **控制流程** ] 索引標籤，然後將 [ **資料流程** ] 工作從 [ **工具箱** ] 拖曳至 [ **控制流程** ] 窗格。  
  
3.  按一下 [**資料流程**] 索引標籤，然後從 [**工具箱**] 將 [一般檔案**來源**] 拖曳至 **[資料流程]** 窗格。 按兩下您剛才建立的方塊以開啟 [一般檔案 **來源編輯器**]。  
  
4.  按一下 [ **連線管理員** ]，然後按一下 [ **新增**]。  
  
5.  在 [ **連接管理員名稱** ] 方塊中，輸入連接的易記名稱。 在此範例中為 `Example Load Flat File CM` 。  
  
6.  按一下 **[流覽]** ，然後 `ExampleLoad.txt` 從本機電腦選取檔案。  
  
7.  由於一般檔案包含具有資料行名稱的資料列，請按一下 **[第一個資料列** ] 方塊中的資料行名稱。  
  
8.  按一下左欄中的 [資料 **行** ]，並預覽將載入的資料，以確保資料行名稱和資料已正確解讀。  
  
9. 在左側資料行中，按一下 [ **Advanced** ]。 按一下每個資料行名稱，以檢查與資料相關聯的資料類型。 在方塊中輸入變更，讓載入資料的資料類型與目的地資料行類型相容。  
  
10. 按一下 **[確定]** 以儲存您的連線管理員。  
  
11. 按一下 **[確定]** 以結束 [一般檔案 **來源編輯器**]。  
  
指定資料流程的目的地。  
  
1.  將 **SQL Server PDW 目的地** 從 [ **工具箱** ] 拖曳至 **[資料流程]** 窗格。  
  
2.  按兩下您剛才建立的方塊以載入 **SQL Server PDW 目的地編輯器**。  
  
3.  按一下 [ **連線管理員**] 旁的向下箭號。  
  
4.  選取 [ **建立新連接**]。  
  
5.  以您設備的特定資訊填入伺服器、使用者、密碼和目的地資料庫的資訊。  (範例如下) 所示。 然後按一下 [確定]  。  
  
    若為 [未連線]， **伺服器名稱**：輸入 <設備名稱>-SQLCTL01，17001。  
  
    針對 [乙太網路連線]，[ **伺服器名稱**]：輸入控制節點叢集的 IP 位址，逗點，埠17001。 例如，10.192.63.134、17001。  
  
    **使用者：**`user1`  
  
    **密碼：**`password1`  
  
    **目的地資料庫：**`LoadExampleDB`  
  
6.  選取目的地資料表： `Orders` 。  
  
7.  選取 [ **附加** ] 作為載入模式，然後按一下 **[確定]**。  
  
指定從來源到目的地的資料流程。  
  
1.  **在 [資料流程] 窗格**中，將 [一般檔案**來源**] 方塊中的綠色箭號拖曳至 [ **SQL Server PDW 目的地**] 方塊。  
  
2.  按兩下 [ **SQL Server PDW 目的地** ] 方塊，讓您再次看到 [ **SQL Server PDW 目的地編輯器** ]。 您應該會在 [未對應的 **輸入資料行**] 下，從左側的一般檔案中看到資料行名稱。 您應該會在 [未對應的 **目的地資料行**] 底下的右邊，看到目的地資料表中的資料行名稱。 藉由拖曳或按兩下未對應的 **輸入資料行** 與未對應的 **目的地資料行** 清單中相符的資料行名稱，將資料行對應至 [ **對應** 的資料行] 方塊。 按一下 [確定] **** 儲存設定。  
  
3.  按一下 [檔案 **] 功能表中的 [** **儲存**]，以儲存封裝。  
  
在您的電腦上執行套件 Integration Services。  
  
1.  在 [Integration Services**方案總管** ] (右側資料行) 中，按一下滑鼠右鍵， `Package.dtsx` 然後選取 [ **執行**]。  
  
2.  封裝將會執行，而且進度和任何錯誤都會顯示在 [ **進度** ] 窗格中。 您可以使用 SQL 用戶端來確認負載，或透過 SQL Server PDW 管理主控台來監視負載。  
  
## <a name="see-also"></a>另請參閱  
[建立使用 SSIS PDW 目的地介面卡的腳本工作](create-ssis-script-task-using-pdw-destination-adapter.md)  
[SQL Server Integration Services](../integration-services/sql-server-integration-services.md)  
[設計和實作封裝 (Integration Services)](https://msdn.microsoft.com/library/ms141091\(v=sql11\).aspx)  
[教學課程：使用精靈建立基本封裝](https://technet.microsoft.com/library/ms365330\(v=sql11\).aspx)  
[消費者入門 (Integration Services) ](https://go.microsoft.com/fwlink/?LinkId=202412)  
[動態套件產生範例](https://go.microsoft.com/fwlink/?LinkId=202413)  
[設計平行處理原則的 SSIS 封裝 (SQL Server 視訊)](/previous-versions/sql/sql-server-2008/dd795221(v=sql.100))  
[Microsoft SQL Server 社區範例： Integration Services](https://go.microsoft.com/fwlink/?LinkId=202415)  
[利用異動資料擷取改善累加式載入](../integration-services/change-data-capture/change-data-capture-ssis.md)  
[緩時變維度轉換](../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)  
[大量插入工作](../integration-services/control-flow/bulk-insert-task.md)  
  
<!-- MISSING LINKS
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examples](metadata-query-examples.md)
-->