---
title: 授與權限的資料來源物件 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.roledesignerdialog.datasources.f1
helpviewer_keywords:
- read/write permissions
- user access rights [Analysis Services], data sources
- security [Analysis Services], data sources
- connection strings [Analysis Services]
- data sources [Analysis Services], security
ms.assetid: b4e302d3-c93b-4383-aa4a-37d15c129830
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4a869d2033adaa57be0ace522787332c03a69bcb
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66074994"
---
# <a name="grant-permissions-on-a-data-source-object-analysis-services"></a>授與資料來源物件的權限 (Analysis Services)
  通常，大部分的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用者都不需要存取 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案的基礎資料來源。 使用者通常只會查詢 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫內的資料。 不過，在資料採礦的內容中，例如要執行以採礦模型為基礎的預測時，使用者就必須聯結採礦模型的所獲得 (Learned) 資料與使用者提供的資料。 若要連接到包含使用者所提供資料的資料來源，使用者要使用包含 [OPENQUERY &#40;DMX&#41;](/sql/dmx/source-data-query-openquery) 和 [OPENROWSET &#40;DMX&#41;](/sql/dmx/source-data-query-openrowset) 子句的資料採礦延伸模組 (DMX) 查詢。  
  
 若要執行連接到資料來源的 DMX 查詢，使用者必須存取 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫內的資料來源物件。 根據預設，只有伺服器管理員或資料庫管理員擁有存取資料來源物件的權限。 這表示除非管理員授與權限，否則使用者無法存取資料來源物件。  
  
> [!IMPORTANT]  
>  基於安全性的考量，在 OPENROWSET 子句中使用開放式連接字串來提交 DMX 查詢的功能已停用。  
  
## <a name="set-read-permissions-to-a-data-source"></a>設定資料來源的讀取權限  
 資料庫角色可以不被授與資料來源物件的任何存取權限，也可以被授與讀取權限。  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，連接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的執行個體，在物件總管中展開適當資料庫的 [角色]，然後按一下資料庫角色 (或建立新的資料庫角色)。  
  
2.  在 [資料來源存取] 窗格的 [資料來源] 清單中尋找資料來源物件，然後在該資料來源的 [存取] 清單中選取 [讀取]。 如果這個選項無法使用，請檢查 [一般] 窗格，以查看是否已選取 [完整控制權]。 [完整控制權] 已經提供權限，您無法覆寫資料來源的權限。  
  
## <a name="working-with-the-connection-string-used-by-a-data-source-object"></a>使用資料來源物件使用的連接字串  
 資料來源物件會包含用於連接到基礎資料來源的連接字串。 此連接字串可指定下列其中之一：  
  
-   **指定使用者名稱和密碼**  
  
     如果資料來源物件使用的連接字串有指定使用者名稱和密碼，您可能需要建立多個資料來源物件，使每一個有不同的使用者帳戶。 建立多個資料來源物件可讓使用者存取特定資料來源物件，及防止該些使用者存取其他資料來源物件。 這些其他資料來源物件可由 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 本身用於處理物件，例如 Cube 和採礦模型。  
  
-   **指定 Windows 驗證**  
  
     如果資料來源物件使用的連接字串指定 Windows 驗證，則 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 必須能夠模擬用戶端。 如果資料來源是在遠端電腦上，就必須使用 Kerberos 驗證來建立兩部電腦之間的信任以進行模擬，否則查詢通常會失敗。 如需詳細資訊，請參閱 [設定 Analysis Services 進行 Kerberos 限制委派](../instances/configure-analysis-services-for-kerberos-constrained-delegation.md) 。  
  
     如果用戶端不容許模擬 (透過 OLE DB 和其他用戶端元件的模擬層級屬性)， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 將會嘗試與基礎資料來源建立匿名連線。 匿名連線遠端資料來源很少成功，因為大部分的資料來源都不接受匿名連線)。  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型中的資料來源](data-sources-in-multidimensional-models.md)   
 [連接字串屬性 &#40;Analysis Services&#41;](../instances/connection-string-properties-analysis-services.md)   
 [Analysis Services 支援的驗證方法](../instances/authentication-methodologies-supported-by-analysis-services.md)   
 [授與維度資料的自訂存取權 &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md)   
 [授與 Cube 或模型權限 &#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md)   
 [授與資料格資料的自訂存取權 &#40;Analysis Services&#41;](grant-custom-access-to-cell-data-analysis-services.md)  
  
  
