---
title: 舊版的 SQL Server Data Tools (SSDT 和 SSDT-BI) | Microsoft Docs
ms.custom: ''
ms.date: 09/05/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 5d32e301-0f44-4916-b0db-76e8322c0ab7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 18b9b09e5437889389f23b32c61b237ab65d3207
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47764416"
---
# <a name="previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi"></a>舊版的 SQL Server Data Tools (SSDT 和 SSDT-BI)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
SQL Server Data Tools (SSDT) 提供專案範本及設計介面以建置 SQL Server 內容類型，包括關聯式資料庫、Analysis Services 模型、Reporting Services 報表以及整合服務套件。  
  
SSDT 可以回溯相容，亦即您可以隨時使用[最新的 SSDT](download-sql-server-data-tools-ssdt.md) 設計及部署要在舊版 SQL Server 上執行的資料庫、模型、報表及套件。  
  
> [!NOTE]  
> 過去會使用 Visual Studio Shell 來建立已用其他各種名稱發行的 SQL Server 內容類型，包括 **SQL Server Data Tools**、 **SQL Server Data Tools - Business Intelligence**以及 **Business Intelligence Development Studio**。 舊版隨附不同的專案範本集。 若要在一個 SSDT 中取得所有專案範本，您需要使用 [最新版本](download-sql-server-data-tools-ssdt.md)。 否則，您可能會需要安裝多個舊版本才能取得 SQL Server 中使用的所有範本。  每個 Visual Studio 版本只會安裝一個 Shell；安裝第二個 SSDT 只會新增缺少的範本。  

## <a name="recent-downloads"></a>最近的下載

我們提供最近幾次下載的相關資訊，以便您在不幸遇到最新版本相關問題時可參考 (雖然這非常不可能發生)。

|SSDT 版本| Visual Studio 2017|
|:---|:---|
|15.8.0|[SSDT for VS2017 15.8.0](https://go.microsoft.com/fwlink/?linkid=2014060)|
|15.7.1|[SSDT for VS2017 15.7.1](https://go.microsoft.com/fwlink/?LinkId=875613)|
|15.7.0|[SSDT for VS2017 15.7.0](https://go.microsoft.com/fwlink/?LinkId=874716)|
|15.6.0|[SSDT for VS2017 15.6.0](https://go.microsoft.com/fwlink/?LinkId=871368)|
<br>

|SSDT 版本| Visual Studio 2015|
|:---|:---|
|17.4|[適用於 VS2015 17.4 的 SSDT](https://go.microsoft.com/fwlink/?linkid=863440)|
|17.3|[適用於 VS2015 17.3 的 SSDT](https://go.microsoft.com/fwlink/?linkid=858660)|
|16.5|[SSDT for VS2015 16.5](https://go.microsoft.com/fwlink/?LinkID=832313)|  
<br>

|SSDT 版本| Visual Studio 2013|
|:---|:---|
|16.5|[SSDT for VS2013 16.5](https://go.microsoft.com/fwlink/?LinkID=832308)|  
<br>


\* SSDT 支援兩個最新版的 Visual Studio。 自 Visual Studio 2017 版起，將不再更新 SSDT for VS2013。 如需其他資訊，請參閱[這篇 SSDT 小組部落格文章](https://blogs.msdn.microsoft.com/ssdt/2017/03/10/sql-server-data-tools-17-0-rc-and-ssdt-in-vs2017/)的 *FAQ* (常見問題集) 一節。

  
## <a name="links-to-download-pages"></a>下載頁面的連結 
**SQL 關聯式：資料庫引擎**  
  
提供範本以建置 RDBMS 和 Azure SQL Database 的關聯式資料庫。 SSDT 版本與關聯式資料庫設計無關。 您可以使用 Visual Studio 2012 或 2013 版本及任何版本的 SQL Server Database Engine 或 Azure SQL Database。  
  
**資料庫設計工具**  
  
-   [下載 SSDT for Visual Studio 2013](https://msdn.microsoft.com/dn864412)  
  
-   [下載 SSDT for Visual Studio 2012](https://msdn.microsoft.com/jj650015)  
  
-   **適用於 Visual Studio 2010 的 SSDT** 已無法再使用，因此，請選擇較新的版本。 較新版本的 SSDT 會與現有的 Visual Studio 2010 安裝並存執行。 SSDT 無須符合您電腦上之 Visual Studio 的完整產品版本。  
  
Visual Studio 2013 的客戶可以下載 SSDT 的預覽版本，試用尚未包含在產品發行版本中的功能。  
  
**SQL BI：Analysis Services、Reporting Services、Integration services**  
  
BI 範本用來建立 SSAS 模型、SSRS 報表及 SSIS 套件。 BI 設計工具與特定版本的 SQL Server 一併發行。 要使用較新的 BI 功能，請安裝較新版本的設計工具。  
  
**BI 設計工具**  
  
[下載 SSDT-BI for Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=42313) (SQL Server 2014、SQL Server 2012、SQL Server 2008 和 2008 R2)  
  
[下載 SSDT-BI for Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=36843) (SQL Server 2014、SQL Server 2012、SQL Server 2008 和 2008 R2)  
  
Business Intelligence Development Studio (BIDS) 是透過 SQL Server 安裝程式安裝。 無法從網路下載。 (SQL Server 2008 和 2008 R2)  
  
對於 SQL Server 2012 或 2014，您可以使用 **適用於 Visual Studio 2012 的 SSDT-BI** 或 **SSDT-BI f或 Visual Studio 2013**。 這兩者的唯一差異是 Visual Studio 版本的不同。  
  
## <a name="see-also"></a>另請參閱  
[下載 SQL Server Data Tools &#40;SSDT&#41;](../ssdt/download-sql-server-data-tools-ssdt.md)  
[下載 SQL Server Management Studio &#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md)  
[SQL 工具和公用程式](../tools/overview-sql-tools.md)
