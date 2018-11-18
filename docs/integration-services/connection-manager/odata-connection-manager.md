---
title: OData 連線管理員 | Microsoft Docs
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.custom: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3caa4372-aff3-4c0f-9ecd-97870948b8d0
f1_keywords:
- sql13.dts.designer.odatasource.connectionmanager.f1
- sql13.dts.designer.odataconnectionmanager.f1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 790c7b1e50b029ab2cf2cbf4ad41bd80cf11cb0c
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/14/2018
ms.locfileid: "51641821"
---
# <a name="odata-connection-manager"></a>OData 連接管理員
 使用 OData 連線管理員連線到 OData 資料來源。 OData 來源元件會使用 OData 連線管理員連線到 OData 資料來源，並取用服務中的資料。 如需詳細資訊，請參閱＜ [OData Source](../../integration-services/data-flow/odata-source.md)＞。  
  
## <a name="adding-an-odata-connection-manager-to-an-ssis-package"></a>將 OData 連接管理員加入 SSIS 封裝中  
 您可以使用三種方式，將新的 OData 連線管理員新增至 SSIS 套件：  
  
-   按一下 [新增…]  按鈕 (位於 [OData 來源編輯器]   
  
-   在 **方案總管** 中，以滑鼠右鍵按一下 [連線管理員] 資料夾，然後按一下 [新增連線管理員] 。 針對 [連線管理員類型]  選取 [ODATA] 。  
  
-   以滑鼠右鍵按一下套件設計師底部的 [連線管理員] 窗格，然後選取 [新增連線…]。 針對 [連線管理員類型]  選取 [ODATA] 。  
  
## <a name="connection-manager-authentication"></a>連接管理員驗證  
 OData 連線管理員支援五種驗證模式。  
  
-   Windows 驗證  
  
-   基本驗證 (使用使用者名稱和密碼)  

-   Microsoft Dynamics AX Online (使用使用者名稱和密碼)
  
-   Microsoft Dynamics CRM Online (使用使用者名稱和密碼)
  
-   Microsoft Online Services (使用使用者名稱和密碼)  
  
如果是匿名存取，請選取 [Windows 驗證] 選項。  

若要連線至 Microsoft Dynamics AX Online 或 Microsoft Dynamics CRM Online，您不能使用 [Microsoft Online Services] 驗證選項。 您也無法使用針對多重要素驗證設定的任何選項。
  
### <a name="specifying-and-securing-credentials"></a>指定認證及維護認證安全  
 如果 OData 服務需要基本驗證，您可以在 [OData 連線管理員編輯器](../../integration-services/connection-manager/odata-connection-manager-editor.md)中指定使用者名稱和密碼。 您在編輯器中輸入的值會保存在封裝中。 密碼值會根據封裝保護等級進行加密。  
  
 有多個方式可將使用者名稱和密碼值參數化，或儲存到封裝外部。 例如，您可以使用參數，或從 SQL Server Management Studio 執行套件時直接設定連線管理員屬性。  
  
## <a name="odata-connection-manager-properties"></a>OData 連接管理員屬性  
 下列清單描述 OData 連線管理員的屬性。  
  
|||  
|-|-|  
|屬性|Description|  
|Url|服務文件的 URL。|  
|UserName|如有必要，驗證使用使用者名稱。|  
|[密碼]|如有必要，驗證使用密碼。|  
|ConnectionString|包括連線管理員的其他屬性。|  
  
## <a name="odata-connection-manager-editor"></a>OData 連線管理員編輯器
  使用 [OData 連線管理員編輯器] 對話方塊新增連線，或編輯現有的 OData 資料來源連線。  
  
### <a name="options"></a>選項。  
 **連線管理員名稱**  
 連接管理員的名稱。  
  
 **服務文件位置**  
 OData 服務的 URL。 例如： https://services.odata.org/V3/Northwind/Northwind.svc/＞。  
  
 **驗證**  
選取下列其中一個選項：
-   **Windows 驗證**。 匿名存取請選取這個選項。
-   **基本驗證** 
-   **Microsoft Dynamics AX Online** for Dynamics AX Online
-   **Microsoft Dynamics CRM Online** for Dynamics CRM Online
-   **Microsoft Online Services** for Microsoft Online Services

如果您選取 Windows 驗證以外的選項，請輸入**使用者名稱**和**密碼**。 

若要連線至 Microsoft Dynamics AX Online 或 Microsoft Dynamics CRM Online，您不能使用 [Microsoft Online Services] 驗證選項。 您也無法使用針對多重要素驗證設定的任何選項。

 **測試連接**  
 按一下此按鈕，測試 OData 來源的連線。  
