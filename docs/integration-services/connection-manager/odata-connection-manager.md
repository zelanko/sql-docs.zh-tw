---
title: "OData 連接管理員 |Microsoft 文件"
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3caa4372-aff3-4c0f-9ecd-97870948b8d0
caps.latest.revision: 9
f1_keywords:
- sql13.dts.designer.odatasource.connectionmanager.f1
- sql13.dts.designer.odataconnectionmanager.f1
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: f54562b59e8c61f723c17e2812ca39cb2e95f273
ms.contentlocale: zh-tw
ms.lasthandoff: 08/28/2017

---
# <a name="odata-connection-manager"></a>OData 連接管理員
 連接到 OData 資料來源的 OData 連接管理員。 OData 來源元件使用 OData 連接管理員連接到 OData 資料來源，並從服務取用資料。 如需詳細資訊，請參閱＜ [OData Source](../../integration-services/data-flow/odata-source.md)＞。  
  
## <a name="adding-an-odata-connection-manager-to-an-ssis-package"></a>將 OData 連接管理員加入 SSIS 封裝中  
 您可以將新的 OData 連接管理員加入 SSIS 封裝三種方式：  
  
-   按一下 [新增…]  按鈕 (位於 [OData 來源編輯器]   
  
-   在 **方案總管** 中，以滑鼠右鍵按一下 [連線管理員] 資料夾，然後按一下 [新增連線管理員] 。 針對 [連線管理員類型]  選取 [ODATA] 。  
  
-   以滑鼠右鍵按一下**連接管理員**窗格底部的 封裝設計工具，然後再選取**新連線**。 針對 [連線管理員類型]  選取 [ODATA] 。  
  
## <a name="connection-manager-authentication"></a>連接管理員驗證  
 OData 連接管理員支援五個模式的驗證。  
  
-   Windows 驗證  
  
-   基本驗證 (使用使用者名稱和密碼)  

-   Microsoft Dynamics AX Online (使用使用者名稱和密碼)
  
-   Microsoft Dynamics CRM Online (使用使用者名稱和密碼)
  
-   Microsoft Online Services (使用使用者名稱和密碼)  
  
如果是匿名存取，請選取 [Windows 驗證] 選項。  

若要連線至 Microsoft Dynamics AX Online 或 Microsoft Dynamics CRM online，您無法使用**Microsoft Online Services**驗證選項。 您也無法使用 multi-factor authentication 設定任何選項。
  
### <a name="specifying-and-securing-credentials"></a>指定認證及維護認證安全  
 如果 OData 服務需要基本驗證，您可以在 [OData 連線管理員編輯器](../../integration-services/connection-manager/odata-connection-manager-editor.md)中指定使用者名稱和密碼。 您在編輯器中輸入的值會保存在封裝中。 密碼值會根據封裝保護等級進行加密。  
  
 有多個方式可將使用者名稱和密碼值參數化，或儲存到封裝外部。 例如，您可以使用參數，或設定連接管理員屬性直接從 SQL Server Management Studio 執行封裝時。  
  
## <a name="odata-connection-manager-properties"></a>OData 連接管理員屬性  
 下列清單描述 OData 連接管理員的屬性。  
  
|||  
|-|-|  
|屬性|說明|  
|Url|服務文件的 URL。|  
|UserName|要用於驗證，如果所需的使用者名稱。|  
|密碼|要用於驗證，如果所需的密碼。|  
|SubQueries|包含連接管理員的其他屬性。|  
  
## <a name="odata-connection-manager-editor"></a>OData 連線管理員編輯器
  使用**OData 連接管理員編輯器**對話方塊來加入連接，或編輯現有的連接到 OData 資料來源。  
  
### <a name="options"></a>選項  
 **連線管理員名稱**  
 連接管理員的名稱。  
  
 **服務文件位置**  
 OData 服務的 URL。 例如：http://services.odata.org/V3/Northwind/Northwind.svc/。  
  
 **驗證**  
選取下列其中一個選項：
-   **Windows 驗證**。 匿名存取，請選取這個選項。
-   **基本驗證** 
-   **線上 Microsoft Dynamics AX**的 Dynamics AX 線上
-   **Microsoft Dynamics CRM Online**的 Dynamics CRM Online
-   **Microsoft Online Services** Microsoft Online services

如果您選取 Windows 驗證以外的選項，輸入**使用者名**和**密碼**。 

若要連線至 Microsoft Dynamics AX Online 或 Microsoft Dynamics CRM online，您無法使用**Microsoft Online Services**驗證選項。 您也無法使用 multi-factor authentication 設定任何選項。

 **測試連接**  
 按一下此按鈕，測試 OData 來源的連接。  

