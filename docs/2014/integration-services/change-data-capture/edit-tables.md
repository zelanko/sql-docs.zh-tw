---
title: 編輯資料表 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- tabProps
ms.assetid: fed8fada-2abc-45e2-8228-0656f9c599cb
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 91424dc726616952a7c4d3f230f845b8ed97f457
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85438715"
---
# <a name="edit-tables"></a>編輯資料表
  使用 **[資料表]** 索引標籤，以變更您從 Oracle 來源資料庫選取的資料表和資料行。 此索引標籤具有以下元素：  
  
 **資料表清單**  
 此資料表清單具有三個資料行：  
  
-   **Oracle 資料表名稱**：資料表的名稱，包括資料表結構描述。  
  
-   **擷取執行個體**：用來命名執行個體特有之異動資料擷取物件的擷取執行個體名稱。 擷取執行個體不得為 NULL。 如果未指定，名稱會衍生自來源結構描述名稱，加上 `<schema-name>_<table-name>.` 格式的來源資料表名稱。擷取執行個體名稱不能超過 100 個字元，而且在資料庫內必須是唯一的。 您可以在此資料行中按一下任何資料格，手動編輯 **capture_instance**。  
  
-   **安全性角色**：用來取得變更資料之存取權的資料庫角色名稱。 您可以在此資料行中按一下任何資料格，手動編輯 **security_role**。  
  
 **加入資料表**  
 按一下 [加入資料表]  開啟 [資料表選取範圍] 對話方塊，即可[將資料表加入至 CDC 執行個體](add-tables-to-a-cdc-instance.md)。 當您初次在此工作階段存取 Oracle 資料庫時，您必須 [Connect to Oracle](connect-to-oracle.md)。  
  
 **編輯**  
 從清單中選取資料表，然後選取 [編輯]  開啟該資料表的 [屬性]  對話方塊，即可[編輯資料表屬性](edit-the-table-properties.md)。  
  
> [!NOTE]  
>  您不能針對已經有鏡像資料表的資料表編輯類型對應。 您只能針對新的資料表編輯類型對應。  
  
 **移除**  
 從清單中選取資料表，並按一下 [移除]  ，從 CDC 執行個體中移除此資料表。  
  
## <a name="see-also"></a>另請參閱  
 [如何編輯 CDC 執行個體屬性](how-to-edit-the-cdc-instance-properties.md)   
 [選取 Oracle 資料表和資料行](select-oracle-tables-and-columns.md)  
  
  
