---
title: 設定資料來源屬性（SSAS 多維度） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.datasourceproperties.f1
helpviewer_keywords:
- Data Source Properties dialog box
ms.assetid: bf8b600f-5b99-4f7d-908b-8a391721e9dd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 76d25aabd5b24cdbcc72d3c356168a040a83081a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66073044"
---
# <a name="set-data-source-properties-ssas-multidimensional"></a>設定資料來源屬性 (SSAS 多維度)
  在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，資料來源物件會指定提供資料給多維度模型之外部資料倉儲或關聯式資料庫的連接。 資料來源屬性決定連接字串、逾時間隔、最大連接數目及交易隔離等級。  
  
## <a name="set-data-source-properties-in-sql-server-data-tools"></a>在 SQL Server Data Tools 中設定資料來源屬性  
  
1.  在 [方案總管] 中，按兩下資料來源開啟 [資料來源設計師]。  
  
2.  按一下 [資料來源設計師] 中的 [模擬資訊]**** 索引標籤。 如需建立資料來源的詳細資訊，請參閱 [建立資料來源 &#40;SSAS 多維度&#41;](create-a-data-source-ssas-multidimensional.md)。  
  
## <a name="set-data-source-properties-in-management-studio"></a>在 Management Studio 中設定資料來源屬性  
  
1.  展開資料庫資料夾，並開啟資料庫名稱底下的 [資料來源]**** 資料夾，然後在**物件總管**中以滑鼠右鍵按一下資料來源，再選取 [屬性]****。  
  
2.  您也可以選擇修改名稱、描述或模擬選項。 如需詳細資訊，請參閱[設定模擬選項 &#40;SSAS - 多維度&#41;](set-impersonation-options-ssas-multidimensional.md)。  
  
## <a name="data-source-properties"></a>資料來源屬性  
  
|詞彙|定義|  
|----------|----------------|  
|**名稱、識別碼、描述**|名稱、識別碼和描述可用來識別及描述多維度模型中的資料來源物件。<br /><br /> 在您部署或處理方案之後，可以在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 或 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中指定名稱和描述。<br /><br /> 識別碼會在建立物件之後產生。 雖然您可以輕鬆地修改名稱和描述，但識別碼是唯讀的，因此不應該變更。 固定物件識別碼會保留整個模型的物件相依性和參照。|  
|**建立時間戳記**|這個唯讀屬性會顯示在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中。 並顯示建立資料來源的日期和時間。|  
|**上次結構描述更新**|這個唯讀屬性會顯示在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中。 並顯示上次更新資料來源之中繼資料的日期和時間。 當您部署方案時，即會更新這個值。|  
|**查詢超時**|指定連接要求在捨棄之前可以嘗試的時間。<br /><br /> 以下列格式鍵入查詢逾時：<br /><br /> 小時>：*\<分鐘>*：*\<秒數>* * \< *<br /><br /> `DatabaseConnectionPoolTimeoutConnection` 伺服器屬性可以覆寫這個屬性。 如果伺服器屬性較小，則會使用這個屬性取代 [查詢逾時]****。<br /><br /> 如需 [**查詢超時**] 屬性的詳細資訊<xref:Microsoft.AnalysisServices.DataSource.Timeout%2A>，請參閱。 如需伺服器屬性的詳細資訊，請參閱 [OLAP 屬性](../server-properties/olap-properties.md)。|  
|**連接字串**|指定提供資料給多維度模型之資料庫的實體位置，以及用於連接的資料提供者。 這項資訊會提供給提出連接要求的用戶端程式庫。 此提供者會決定可在連接字串上設定的屬性。<br /><br /> 連接字串使用您在 [連線管理員]**** 對話方塊中提供的資訊建立。 您也可以在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 的資料來源屬性頁面中，檢視及編輯連接字串。<br /><br /> 對於 SQL Server 資料庫而言，包含 `user ID` 的連接字串表示資料庫驗證，而包含 `Integrated Security=SSPI` 的連接表示 Windows 驗證。<br /><br /> 如果將資料庫移至新位置，則可以變更伺服器或資料庫名稱。 請務必確認目前為連接指定的認證對應至資料庫登入。|  
|**最大連接數目**|指定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 允許連接至資料來源的最大連接數目。 如果需要更多連接數目， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會等到可以使用連接。 預設值為 10。 限制連接數目可確保外部資料來源不會因 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 要求而超過負載。|  
|**實施**|指定關聯式資料庫的連接所發出之 SQL 命令的鎖定和資料列版本設定行為。 有效值是 ReadCommitted 或快照集。 預設值是 ReadCommitted，指定在讀取資料之前必須認可資料，以避免中途讀取。 快照集指定從先前認可之資料的快照集讀取。 如需 SQL Server 之隔離等級的詳細資訊，請參閱 [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql)。|  
|**Managed 提供者**|如果資料來源使用 Managed 提供者，則顯示 Managed 提供者的名稱，例如 System.Data.SqlClient 或 System.Data.OracleClient。<br /><br /> 如果資料來源未使用 Managed 提供者，此屬性就會顯示空的字串。<br /><br /> 這個屬性在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中是唯讀的。 若要變更用於連接的提供者，請編輯連接字串。|  
|**模擬資訊**|指定連接至使用 Windows 驗證的資料來源時，執行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的 Windows 識別。 這些選項包括使用一組預先定義的 Windows 認證、服務帳戶、目前使用者的識別，或適用於模型包含多個資料來源物件的繼承選項。 如需詳細資訊，請參閱[設定模擬選項 &#40;SSAS - 多維度&#41;](set-impersonation-options-ssas-multidimensional.md)。<br /><br /> 在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中，有效值清單包含這些值：<br /><br /> **ImpersonateAccount** (使用特定的 Windows 使用者名稱和密碼來連接到資料來源)。<br /><br /> **ImpersonateServiceAccount** (使用服務帳戶的安全性識別來連接到資料來源)。 這是預設值。<br /><br /> **ImpersonateCurrentUser** (使用目前使用者的安全性識別來連接到資料來源)。 這個選項只對從外部資料倉儲或資料庫擷取資料的資料採礦查詢才有效；對於在多維度資料庫中處理、載入或回寫所使用的資料連接，請勿選擇這個選項。<br /><br /> [繼承]**** 或 [預設值]**** (使用包含此資料來源物件之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫的模擬設定)。 資料庫屬性包括模擬選項。|  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型中的資料來源](data-sources-in-multidimensional-models.md)   
 [建立資料來源 &#40;SSAS 多維度&#41;](create-a-data-source-ssas-multidimensional.md)  
  
  
