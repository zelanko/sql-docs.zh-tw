---
title: 第 4 課：在 MDS 中儲存供應商資料 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: bacd9eaf-4d12-4f25-aec7-d785dec1b623
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 678a7d6ce075e6a1082856aa7962bb3f6eec522d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65489712"
---
# <a name="lesson-4-storing-supplier-data-in-mds"></a>第 4 課：在 MDS 中儲存供應商資料
  Master Data Services (MDS) 是用於主要資料管理的 SQL Server 解決方案。 主要資料管理 (MDM) 會描述組織為了探索及定義非交易之資料清單所付出的心力。  
  
 模型是 Master Data Services 中的最高組織層級，而且會組織主要資料的結構。 您的 MDS 實作可以有一個或多個模型，其中每個模型都會將類似資料分組在一起。 主要資料通常以四種方式分類：人員、位置、東西或概念。 例如，您可以建立一個 Product 模型來容納產品相關的資料，或是建立一個 Customer 模型來容納客戶相關的資料。 請參閱[模型 (Master Data Services)](https://msdn.microsoft.com/library/ee633746.aspx)如需詳細資訊。  
  
 模型可以包含一個或多個實體。 每個實體都有屬性 (資料行) 和成員 (資料列)。 每個資料列都包含主要資料。 在這一課，您會建立一個 Suppliers 模型，此模型包含名為 Supplier 和 State 的兩個實體。 Supplier 實體將具有下列屬性：程式碼、 名稱、 Contact First Name、 Contact Last Name、 連絡電子郵件地址、 地址、 縣 （市）、 狀態、 Zip、 和國家/地區。 請參閱[屬性 (Master Data Services)](https://msdn.microsoft.com/library/ee633745.aspx)如需詳細資料屬性的相關一般。 Code 和 Name 屬性會對應至 Cleansed and Matched Suppliers Excel 檔案中的 [SupplierID] 和 [Supplier Name] 資料行。  
  
 定義域屬性是由其他實體成員填入其值的屬性。 網域屬性可防止使用者輸入無效的屬性值。 屬性值只能從另一個實體所擴展的下拉式清單來選取。 在本教學課程中，Supplier 實體的 State 屬性是包含 State 實體中之值的定義域屬性。 您只能將 Supplier 實體的 State 屬性值變更為 State 實體中的其中一個值。 請參閱[網域型屬性](../master-data-services/domain-based-attributes-master-data-services.md)如需詳細資訊。  
  
 MDS 中的衍生階層衍生自模型中的定義域屬性關聯性。 在本教學課程中，您建立 Supplier 實體與 State 實體之間的衍生階層。 在您建立衍生階層之後，您會在主資料管理員的瀏覽器中看到州別清單。 當您按一下清單中的某一州時，您會在右窗格中看到位於該州的供應商。 您之後會根據這個關聯性建立衍生階層。 請參閱[衍生階層](../master-data-services/derived-hierarchies-master-data-services.md)如需詳細資訊。  
  
 您已在 DQS 中建立知識庫，並使用它來清理和比對供應商資料，並將結果儲存在 Cleansed and Matched Supplier Data.xls 檔案中。 在這一課，您將已清理和比對的資料上傳到 MDS。 DQS 僅包含有關資料 (中繼資料) 的知識，而 MDS 則會儲存資料本身 (主要集合)。 例如：DQS 可能擁有有關數家供應商的知識，但是 MDS 只會維護一家公司使用供應商。  
  
 在這一課，您會執行下列工作：  
  
1.  建立**供應商**中的模型**MDS**利用**主資料管理員 Web 應用程式**。  
  
2.  開啟**Cleansed and Matched Supplier Data.xls**在 Excel 中並使用**MDS 增益集適用於 Excel**來建立名為實體**供應商**並將資料上傳至 MDS。  
  
3.  確認資料已建立在 MDS 中，使用**主資料管理員**。  
  
4.  建立名為實體**狀態**，並更新**狀態**屬性**供應商**是取決於網域型屬性的實體**狀態**實體。 您可以執行所有使用此**MDS 增益集適用於 Excel**。  
  
5.  確認使用建立網域屬性**主資料管理員**及更新的值**名稱**屬性**狀態**實體。  
  
6.  檢視使用您所進行的更新**主資料管理員**中**Excel**。  
  
7.  從值載入**狀態**實體載入**Excel**加入值，並使用驗證新增**主資料管理員**。  
  
8.  建立及使用衍生的階層之間的網域屬性關聯性**供應商**實體並**狀態**實體 （Supplier 實體的 State 屬性為 State 實體的類型) 使用**主資料管理員**。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 1：建立使用主資料管理員的供應商模型](../../2014/tutorials/task-1-creating-suppliers-model-using-master-data-manager.md)  
  
  
