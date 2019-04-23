---
title: SQL Server 平行處理資料倉儲連線類型 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 3925fd3d-2aa1-4768-96ad-cfc2c0ba9283
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c628f8c853879a4c601e1c9529f97fd7877551df
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59969314"
---
# <a name="sql-server-parallel-data-warehouse-connection-type-ssrs"></a>SQL Server Parallel Data Warehouse 連接類型 (SSRS)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssDWCurrentFull](../../../includes/ssdwcurrentfull-md.md)] 是可擴充的資料倉儲應用裝置，透過大量平行處理提供效能和擴充性。 [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] 使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 資料庫來進行分散式處理和資料存放。  
  
 此應用裝置會將大型資料庫資料表分割到多個實體節點，每個節點均執行其各自的 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]執行個體。 當報表連接至 [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] 以擷取報表資料時，它會連接至 [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] 應用裝置中負責管理查詢處理的控制節點。 建立連接之後，使用在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 環境內和不在該環境中的 [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] 執行個體便無差別。  
  
 若要在報表中包含來自 [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] 的資料，您必須具有以 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 平行資料倉儲類型之報表資料來源為基礎的資料集。 這個內建的資料來源類型是以 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 平行處理資料倉儲資料延伸模組為基礎。 使用此資料來源類型可連接至 [!INCLUDE[ssDW](../../../includes/ssdw-md.md)]並從中擷取資料。  
  
 此資料延伸模組支援多值參數、伺服器彙總，以及與連接字串分開管理的認證。  
  
 如需詳細資訊，請參閱 [SQL Server 2008 R2 平行資料倉儲](https://go.microsoft.com/fwlink/?LinkId=150895)網站。  
  
 您可以使用本主題中的資訊來建置資料來源。 如需逐步指示，請參閱 <<c0> [ 加入及驗證資料連接或資料來源&#40;報表產生器及 SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)。</c0>  
  
##  <a name="Connection"></a> 連接字串  
 當您連接到 [!INCLUDE[ssDW](../../../includes/ssdw-md.md)]時，是連接到 [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] 應用裝置內的資料庫物件。 您會指定在查詢設計工具中使用的資料庫物件。 如果您未在連接字串中指定資料庫，則會連接到管理員指派給您的預設資料庫。 請洽詢資料庫管理員，以取得用來連接資料來源的連接資訊和認證。 下列連接字串範例會指定 **應用裝置中的範例資料庫**CustomerSales [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] ：  
  
```  
HOST=<IP address>; database= CustomerSales; port=<port>  
```  
  
 此外，您會使用 **[資料來源屬性]** 對話方塊來提供使用者和密碼等認證。 `User Id` 和 `Password` 選項會自動附加到連接字串，您不必隨連接字串一起輸入它們。 使用者介面也會提供選項來指定 [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] 應用裝置中控制節點的 IP 位址以及通訊埠編號。 通訊埠依預設為 17000。 管理員可設定此通訊埠，而您的連接字串可能會使用不同的通訊埠編號。  
  
 如需連接字串範例的詳細資訊，請參閱 [報表產生器中的資料連接、資料來源及連接字串](../data-connections-data-sources-and-connection-strings-in-report-builder.md)。  
  
##  <a name="Credentials"></a> 認證  
 [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] 採用內建的安全性技術來實作及儲存使用者名稱和密碼。 您無法使用 Windows 驗證。 如果您嘗試使用 Windows 驗證連接到 [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] ，就會發生錯誤。  
  
 您必須有足夠的認證才能存取資料庫。 根據查詢而定，您可能還需要其他權限，例如存取資料表和檢視表的足夠權限。 外部資料來源的擁有者必須設定認證，而這些認證必須足以提供您所需資料庫物件的唯讀存取權。  
  
 報表撰寫用戶端提供下列可用來指定認證的選項：  
  
-   使用預存的使用者名稱和密碼。 為了交涉在資料庫包含的報表資料不同於報表伺服器時發生的雙躍點，請選取使用認證做為 Windows 認證的選項。 您也可以選擇在連接到資料來源之後模擬已驗證的使用者。  
  
-   不需要認證。 若要使用這個選項，您先前必須在報表伺服器上設定自動執行帳戶。 如需詳細資訊，請參閱 msdn.microsoft.com 上 [Reporting Services 文件](https://go.microsoft.com/fwlink/?linkid=121312)中的[設定自動執行帳戶 &#40;SSRS 設定管理員&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)。  
  
 如需詳細資訊，請參閱 <<c0> [ 資料連接、 資料來源和 Reporting Services 中的連接字串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)或是[在 報表產生器中指定認證](../specify-credentials-in-report-builder.md)。  

##  <a name="Query"></a> 查詢  
 查詢會指定要為報表資料集擷取的資料。  
  
 查詢結果集中的資料行會填入資料集的欄位集合。 如果查詢傳回多個結果集，報表只會處理查詢擷取的第一個結果集。 根據預設，如果您建立新查詢或開啟現有查詢，而查詢可在圖形化查詢設計工具中表示，就可使用關聯式查詢設計工具。 您可以利用下列方式指定查詢：  
  
-   以互動方式建立查詢。 使用關聯式查詢設計工具，顯示資料表、檢視表和其他資料庫項目的階層式檢視 (依資料庫結構描述組織)。 從資料表或檢視表選取資料行 藉由指定篩選準則、群組和彙總，限制要擷取的資料列數目。 藉由設定參數選項，在報表執行時自訂篩選器。  
  
-   輸入或貼上查詢。 使用以文字為基礎的查詢設計工具直接輸入 [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] 文字、從另一個來源貼上查詢文字、輸入不能利用關聯式查詢設計工具建立的複雜查詢，或是輸入以查詢為基礎的運算式。  
  
-   從檔案或報表匯入現有的查詢。 使用查詢設計工具的 **[匯入查詢]** 按鈕瀏覽至 .sql 檔案或 .rdl 檔案，然後匯入查詢。  
  
 如需詳細資訊，請參閱[關聯式查詢設計工具使用者介面 &#40;報表產生器&#41;](relational-query-designer-user-interface-report-builder.md) 和[以文字為基礎的查詢設計工具使用者介面 &#40;報表產生器&#41;](text-based-query-designer-user-interface-report-builder.md)。  
  
 以文字為基礎的查詢設計工具支援 [文字](#QueryText) 模式，在此模式下，您可以輸入從資料來源選取資料的 [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] 命令。  
  
-   [文字](#QueryText)  
  
 您可以使用 [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] 搭配 [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] 以及 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 搭配 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]。 這兩種 SQL 語言方言非常類似。 針對 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料來源連接類型撰寫的查詢，通常可用於 [!INCLUDE[ssDWCurrentFull](../../../includes/ssdwcurrentfull-md.md)] 資料來源連接類型。  
  
 若查詢是從大型資料庫 (包括 [!INCLUDE[ssDW](../../../includes/ssdw-md.md)]的資料倉儲) 擷取報表資料，它產生的結果集可能具有非常大量的資料列，除非您彙總和摘要資料來減少查詢傳回的資料列數。 您可以使用圖形化或以文字為基礎的查詢設計工具來撰寫包含彙總和群組的查詢。  
  
 [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] 支援查詢設計工具提供用於摘要資料的子句、關鍵字和彙總。  
  
 [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] 使用的圖形化查詢設計工具提供群組和彙總的內建支援，可協助您撰寫只擷取摘要資料的查詢。 [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] 語言功能包括 GROUP BY 子句、DISTINCT 關鍵字以及如 SUM 和 COUNT 等彙總。 以文字為基礎的查詢設計工具提供 [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] 語言的完整支援，包括群組和彙總。  
  
 如需 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 的詳細資訊，請參閱 msdn.microsoft.com 上《[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [線上叢書》](https://go.microsoft.com/fwlink/?LinkId=141687)中的 [Transact-SQL 參考 &#40;資料庫引擎&#41;](/sql/t-sql/language-reference)。  
  
###  <a name="QueryText"></a> 使用 Text 查詢類型  
 在以文字為基礎的查詢設計工具中，您可以輸入 [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] 命令來定義資料集內的資料。 您用來從 [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] 擷取資料的查詢，與用來從不是在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 應用程式中執行之 [!INCLUDE[ssDW](../../../includes/ssdw-md.md)] 執行個體擷取資料的查詢相同。 例如，下列 [!INCLUDE[DWsql](../../../includes/dwsql-md.md)] 查詢會選取所有行銷助理員工的名字：  
  
```  
SELECT  
  HumanResources.Employee.BusinessEntityID  
  ,HumanResources.Employee.JobTitle  
  ,Person.Person.FirstName  
  ,Person.Person.LastName  
FROM  
  Person.Person  
  INNER JOIN HumanResources.Employee  
    ON Person.Person.BusinessEntityID = HumanResources.Employee.BusinessEntityID  
WHERE HumanResources.Employee.JobTitle = 'Marketing Assistant'   
```  
  
 按一下工具列上的 **[執行]** 按鈕 (**!**) 來執行查詢並顯示結果集。  
  
 若要將這個查詢參數化，請加入查詢參數。 例如，將 WHERE 子句變更為下列：  
  
 `WHERE HumanResources.Employee.JobTitle = (@JobTitle)`  
  
 當您執行查詢時，會自動建立與查詢參數對應的報表參數。 如需詳細資訊，請參閱本主題稍後的 [查詢參數](#Parameters) 。  

##  <a name="Parameters"></a> 參數  
 當查詢文字包含具有輸入參數的查詢變數或預存程序時，會自動產生資料集的對應查詢參數和報表的報表參數。 查詢文字的查詢變數不能包含 DECLARE 陳述式。  
  
 例如，下列 SQL 查詢會建立名為 `EmpID` 的報表參數：  
  
```  
SELECT FirstName, LastName FROM HumanResources.Employee E INNER JOIN  
       Person.Contact C ON  E.ContactID=C.ContactID   
WHERE EmployeeID = (@EmpID)  
```  
  
 根據預設，每個報表參數的資料類型為 Text，並具有自動建立的資料集，以提供可用值的下拉式清單。 建立報表參數後，您可能必須變更預設值。 如需詳細資訊，請參閱 MSDN 上的 [報表參數 &#40;報表產生器和報表設計師&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)類型之報表資料來源為基礎的資料集。  

##  <a name="Remarks"></a> 備註  
  
###### <a name="platform-and-version-information"></a>平台和版本資訊  
 如需平台和版本支援的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [ 線上叢書》](https://go.microsoft.com/fwlink/?linkid=121312)中 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 文件的 [Reporting Services &#40;SSRS&#41; 支援的資料來源](../create-deploy-and-manage-mobile-and-paginated-reports.md)。  

##  <a name="HowTo"></a> 如何主題  
 本節包含使用資料連接、資料來源與資料集的逐步指示。  
  
 [加入及驗證資料連接或資料來源&#40;報表產生器及 SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [建立共用資料集或內嵌資料集 &#40;報表產生器及 SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [將篩選加入資料集中 &#40;報表產生器及 SSRS&#41;](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  

##  <a name="Related"></a> 相關章節  
 本文件集的這些章節會提供報表資料的深入概念性資訊，以及如何定義、自訂和使用與報表資料相關組件的程序資訊。  
  
 [將資料加入至報表&#40;報表產生器及 SSRS&#41;](report-datasets-ssrs.md)  
 提供存取報表資料的概觀。  
  
 [報表產生器中的資料連接、資料來源及連接字串](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
 提供資料連接與資料來源的相關資訊。  
  
 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 提供內嵌與共用資料集的相關資訊。  
  
 [資料集欄位集合 &#40;報表產生器及 SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)  
 提供查詢所產生之資料集欄位集合的相關資訊。  
  
 《[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [線上叢書》](https://go.microsoft.com/fwlink/?linkid=121312)中 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 文件的 [Reporting Services 支援的資料來源 &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md)。  
 提供支援每一個資料延伸模組之平台與版本的深入資訊。  

## <a name="see-also"></a>另請參閱  
 [報表參數 &#40;報表產生器和報表設計師&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [運算式 &#40;報表產生器及 SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
