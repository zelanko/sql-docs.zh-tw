---
title: Analysis Services 中表格式模型的相容性層級 |Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fd70a673744d2e401e8a28f6ce2c533434e1c75e
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2019
ms.locfileid: "63472304"
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a>Analysis Services 表格式模型的相容性層級
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

  *相容性層級*指的是 Analysis Services 引擎中的特定版本的行為。 比方說，DirectQuery 和表格式物件中繼資料根據相容性層級上有不同的實作。 在一般，您應該選擇支援您的伺服器最新的相容性層級。

  **最新的相容性層級是 1400** 
  
在 1400年相容性層級中的主要功能包括：

*  新的基礎結構進行資料連接，並匯入表格式模型支援 TOM Api 和 TMSL 指令碼。 這可讓其他資料來源，例如 Azure Blob 儲存體的支援。 其他資料來源會包含在未來更新中。
*  資料轉換和資料混搭功能在 SSDT 中使用 Get Data 與 M 運算式。
*  量值現在支援使用 DAX 運算式，啟用 BI 工具，例如 Microsoft Excel，向下鑽研到詳細資料，從彙總的報表的詳細資料列屬性。 例如，當使用者檢視區域和月份的總銷售額，他們可以檢視相關聯的訂單詳細資料。 
*  資料表和資料行的名稱，其中的資料和物件層級安全性。
*  不完全階層的增強的支援。
*  效能和監控改善。

  
## <a name="supported-compatibility-levels-by-version"></a>版本所支援的相容性層級
  
|||  
|-|-|- 
|**相容性層級**|**伺服器版本**| 
|1400|Azure Analysis Services, SQL Server 2017 |  
|1200|Azure Analysis Services, SQL Server 2017, SQL Server 2016| 
|1103|SQL Server 2017*, SQL Server 2016, SQL Server 2014, SQL Server 2012 SP1|  
|1100|SQL Server 2017 *，SQL Server 2016、 2014年的 SQL Server、 SQL Server 2012 SP1、 SQL Server 2012| 

\* SQL Server 2017 中已被取代 1100年和 1103年相容性層級。
  
## <a name="set-compatibility-level"></a>設定相容性層級 
 當在 SQL Server Data Tools (SSDT) 建立新的表格式模型專案，您可以指定相容性層級上**表格式模型設計師**對話方塊。 
  
 ![ssas_tabularproject_compat1200](../../analysis-services/tabular-models/media/ssas-tabularproject-compat1200.png)  
  
 如果您選取**不要再顯示此訊息**選項，所有後續專案會使用您指定為預設相容性層級。 您可以變更在 SSDT 中的預設相容性層級**工具** > **選項**。  
  
 若要升級 SSDT 中的表格式模型專案時，將**相容性層級**模型中的屬性**屬性**視窗。 請記住，升級相容性層級是無法復原。
  
## <a name="check-compatibility-level-for-a-database-in-ssms"></a>在 SSMS 中檢查表資料庫的相容性層級  
 在 SSMS 中，以滑鼠右鍵按一下資料庫名稱 >**屬性** > **相容性層級**。  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a>在 SSMS 中檢查伺服器支援的相容性層級  
 在 SSMS 中，以滑鼠右鍵按一下伺服器名稱 >**屬性** > **支援的相容性層級**。  
  
 此屬性指定的資料庫，將會在伺服器上執行的最高的相容性層級。 支援的相容性層級是唯讀且無法變更。  
  
## <a name="see-also"></a>另請參閱  
 [多維度資料庫的相容性層級](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [What's new in Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md)   
 [建立新的表格式模型專案](../../analysis-services/tabular-models/create-a-new-tabular-model-project-analysis-services.md)  
  
  
