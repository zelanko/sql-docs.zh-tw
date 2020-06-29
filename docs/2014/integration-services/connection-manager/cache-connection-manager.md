---
title: 快取連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Cache connection manager
ms.assetid: bdc92038-3720-4795-8a5c-79b963f2c952
author: chugugrace
ms.author: chugu
ms.openlocfilehash: efa77442292b66f72886c8dad84e14df3ee0f985
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85434235"
---
# <a name="cache-connection-manager"></a>快取連接管理員
  快取連接管理員會從快取轉換或快取檔案 (.caw) 中讀取資料，而且可以將資料儲存至快取檔案。 不論您是否將快取連接管理員設定為使用快取檔案，資料一定會儲存在記憶體中。  
  
 「快取轉換」轉換會將資料流程中已連接之資料來源的資料寫入快取連接管理員。 封裝中的「查閱」轉換會在資料上執行查閱。  
  
> [!NOTE]  
>  快取連接管理員不支援二進位大型物件 (BLOB) 資料類型 DT_TEXT、DT_NTEXT 和 DT_IMAGE。 如果參考資料集包含 BLOB 資料類型，則在您執行封裝時元件會失敗。 您可以使用 **[快取連接管理員編輯器]** 修改資料行資料類型。 如需詳細資訊，請參閱 [快取連線管理員編輯器](../cache-connection-manager-editor.md)。  
  
> [!NOTE]  
>  封裝保護等級不會套用至快取檔案。 如果快取檔案包含機密資訊，請使用存取控制清單 (ACL) 限制對其中儲存檔案的位置或資料夾的存取權。 您應該只啟用特定帳戶的存取權。 如需詳細資訊，請參閱 [對封裝使用之檔案的存取權](../access-to-files-used-by-packages.md)。  
  
## <a name="configuration-of-the-cache-connection-manager"></a>快取連接管理員的組態  
 您可以利用下列方式設定快取連接管理員：  
  
-   指出是否要使用快取檔案。  
  
     如果您將快取連接管理員設定為使用快取檔案，連接管理員將進行下列其中一項動作：  
  
    -   當「快取轉換」轉換設定為將資料流程中資料來源的資料寫入快取連接管理員時，將資料儲存至檔案。  
  
    -   從快取檔案中讀取資料。  
  
     如需詳細資訊，請參閱 [Cache Transform](../data-flow/transformations/cache-transform.md)。  
  
-   變更儲存在快取中的資料行的中繼資料。  
  
-   在執行階段更新快取檔案名稱，其方法是使用運算式來設定 ConnectionString 屬性。 如需詳細資訊，請參閱 [在封裝中使用屬性運算式](../expressions/use-property-expressions-in-packages.md)。  
  
 您可以透過 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需可在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 設計師中設定之屬性的詳細資訊，請參閱 [快取連線管理員編輯器](../cache-connection-manager-editor.md)。  
  
 如需如何以程式設計方式設定連線管理員的資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和[以程式設計方式新增連線](../building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="related-tasks"></a>相關工作  
 [使用快取連線管理員以完整快取模式實作查閱轉換](lookup-transformation-full-cache-mode-ole-db-connection-manager.md)  
  
  
