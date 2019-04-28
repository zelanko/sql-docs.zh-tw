---
title: OData 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3caa4372-aff3-4c0f-9ecd-97870948b8d0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0b0596e9ba13e617b6f4eef961966bcc07107314
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62833106"
---
# <a name="odata-connection-manager"></a>OData 連接管理員
  OData 連接管理員可讓封裝連接到 OData 來源。 OData 來源元件會使用 OData 連接管理員連接到 OData 來源，並取用此服務中的資料。 請參閱[OData 來源](../data-flow/odata-source.md)一節以取得詳細資訊，包括這些元件的安裝指示。  
  
## <a name="adding-connection-manager-to-an-ssis-package"></a>將連接管理員加入至 SSIS 封裝  
 您可以使用三種方式，將新的 OData 連接管理員加入至 SSIS 封裝：  
  
-   按一下 [OData 來源編輯器] 中的 [新增...] 按鈕  
  
-   以滑鼠右鍵按一下**連接管理員**資料夾中的**方案總管**，按一下 **新的連接管理員**。 針對 [連線管理員類型]  選取 [ODATA] 。  
  
-   以滑鼠右鍵按一下**連接管理員**] 窗格底部的 [封裝設計工具，然後選取**新增連接...**.針對 [連線管理員類型]  選取 [ODATA] 。  
  
## <a name="connection-manager-authentication"></a>連接管理員驗證  
 OData 連接管理員支援兩種模式的驗證。  
  
-   Windows 驗證  
  
-   基本驗證 (使用者名稱/密碼)  
  
 如果是匿名存取，請選取 [Windows 驗證] 選項  
  
### <a name="specifying-and-securing-credentials"></a>指定認證及維護認證安全  
 如果您的 OData 服務需要基本驗證，您可以指定使用者名稱和密碼[OData 連線管理員編輯器](../odata-connection-manager-editor.md)。 您在編輯器中輸入的值會保存在封裝中。 密碼值會根據封裝保護等級進行加密。  
  
 有多個方式可將使用者名稱和密碼值外部化/參數化。 當您使用 SQL Server Management Studio 執行封裝時，在 [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)] 中執行這項處理的兩個主要方式是藉由使用參數或是直接設定連接管理員屬性。  
  
## <a name="odata-connection-manager-properties"></a>OData 連接管理員屬性  
 下列清單描述您可能想要變更的一些 OData 連接管理員屬性。  
  
|||  
|-|-|  
|屬性|描述|  
|Url|服務文件的 URL。|  
|UserName|基本驗證所使用的使用者名稱。|  
|[密碼]|基本驗證所使用的密碼。|  
|ConnectionString|反映連接管理員的其他屬性。|  
  
## <a name="see-also"></a>另請參閱  
 [OData 連線管理員編輯器](../odata-connection-manager-editor.md)  
  
  
