---
title: SQL Server 2014 中已停止的 Master Data Services 功能 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 3236cce0-cfd9-43f8-8be3-e8c8dff8f162
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 3f1eb85cb05c8284990d46241ed752515ef5504b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "65479447"
---
# <a name="discontinued-master-data-services-features-in-sql-server-2014"></a>SQL Server 2014 中已停止的 Master Data Services 功能
  本主題描述 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 中不再可用的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]功能。  
  
## <a name="sssql14-discontinued-features"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 已停止的功能  
 這一版沒有已停止的功能。  
  
## <a name="sssql11-discontinued-features"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 已停止的功能  
  
### <a name="security"></a>安全性  
 若要讓安全性的指派更為容易，您可以不再將模型物件權限指派給 [衍生階層]、[明確階層] 和 [屬性群組] 物件。  
  
-   衍生階層權限現在是以模型為基礎。 例如，如果您想要讓使用者擁有衍生階層的許可權，則必須將**更新**指派給模型物件。 接著，您可以將**拒絕**存取權指派給您不想讓使用者存取的任何實體。  
  
-   明確階層權限現在是以實體為基礎。 例如，如果使用者具有帳戶實體的 [**更新**] 許可權，則該實體的所有明確階層都是可更新的。  
  
-   在 [**使用者和群組的許可權**] 功能區域中，無法再指派屬性群組許可權。 相反地，在建立屬性群組的 [**系統管理**] 功能區域中，使用者和群組可以獲得屬性群組的 [**更新**] 許可權。 屬性群組的**唯讀**許可權已無法再使用。  
  
### <a name="staging-process"></a>暫存處理序  
 您不能使用新的暫存處理序來：  
  
-   建立或刪除集合。  
  
-   在集合中加入或移除成員。  
  
-   重新啟用成員和集合。  
  
 您可以使用 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 暫存處理序來搭配集合一起運作。  
  
### <a name="model-deployment-wizard"></a>模型部署精靈  
 包含資料的封裝無法再使用 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式中的精靈加以建立及部署。 但可以改用新的命令列公用程式。 如需詳細資訊，請參閱[部署模型 &#40;Master Data Services&#41;](deploying-models-master-data-services.md)。  
  
 此精靈依然可用來建立及部署不含資料的封裝。  
  
 此外，封裝只能部署到之前建立封裝所使用的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本。 這表示，在 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 中建立的封裝無法部署到 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]。 您必須將封裝部署到 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 環境，然後將資料庫升級到 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]。  
  
### <a name="code-generation-business-rules"></a>代碼產生商務規則  
 自動為代碼屬性產生值的商務規則現在會以不同的方式管理。 先前，若要產生 Code 屬性的值，您在 [**商務規則**] 下的 [**系統管理**] 功能區域中，使用了 [預設屬性] 做為 [**產生的值**] 動作。 現在，在 [**系統管理**] 中，您必須編輯實體以啟用自動產生的程式碼值。 如需詳細資訊，請參閱[自動建立程式碼 &#40;Master Data Services&#41;](automatic-code-creation-master-data-services.md)。  
  
 如果您擁有包含此類型之規則的 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 模型部署封裝，當您將資料庫升級到 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 時，將會排除此商務規則。  
  
### <a name="bulk-updates-and-exporting"></a>大量更新及匯出  
 在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式中，您無法再針對多個成員大量更新屬性值。 若要執行大量更新，請使用暫存進程或[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]。  
  
 在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式中，您無法再將成員匯出到 Excel 中。 若要在 Excel 中使用成員，請[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]使用。  
  
### <a name="transactions"></a>異動  
 在 [ **Explorer** ] 功能區域中，使用者無法再還原自己的交易。 之前，使用者可以還原他們對**Explorer**中資料所做的變更。 系統管理員仍然可以還原 [**版本管理**] 功能區域中所有使用者的交易。  
  
 註解現在是永久的，而且無法刪除。 先前系統會將註解視為交易，因此可以透過還原交易來刪除。  
  
### <a name="web-service"></a>Web 服務  
 如 Silverlight 所要求，系統現在會自動啟用 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web 服務。 先前必須手動啟用 Web 服務。  
  
### <a name="powershell-cmdlets"></a>PowerShell Cmdlet  
 MDS 不再包含 PowerShell 指令程式。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2014 中已被取代的 Master Data Services 功能](deprecated-master-data-services-features.md)  
  
  
