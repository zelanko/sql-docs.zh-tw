---
title: 設定 In-memory 或 DirectQuery 表格式模型資料庫的存取 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a5d439a9-5be1-4145-90e8-90777d80e98b
caps.latest.revision: 5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ee6b2f55d1b630b489f65e16a39cb602d5fd5a6d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37243438"
---
# <a name="configure-in-memory-or-directquery-access-for-a-tabular-model-database"></a>為表格式模型資料庫設定 In-Memory 或 DirectQuery 存取
  本主題描述如何變更已經部署之表格式模型的連接屬性，以便在 DirectQuery 模式中啟用此模型。  
  
 如需有關這些屬性和組態的最常見的案例的詳細資訊，請參閱 < [DirectQuery 部署案例&#40;SSAS 表格式&#41;](../directquery-deployment-scenarios-ssas-tabular.md)。  
  
## <a name="requirements"></a>需求  
 在表格式模型中啟用 DirectQuery 模式為多步驟的程序。 您必須：  
  
1.  確定此模型並沒有任何功能可能在 DirectQuery 模式中造成驗證錯誤。  
  
2.  在此模型上變更儲存模式來支援 DirectQuery。  
  
3.  在支援混合或純 DirectQuery 模式之查詢的模式中部署此模型。  
  
4.  在部署的資料庫上編輯連接字串，以支援 DirectQuery 模式。  
  
 本主題假設您已經建立和驗證您的模型，而且只需要從類似 [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] 的用戶端啟用 DirectQuery 存取。  
  
## <a name="procedure"></a>程序  
  
#### <a name="change-the-connection-string-properties-of-the-model"></a>變更模型的連接字串屬性  
  
1.  在 SQL Server Management Studio 中，開啟部署模型的目標執行個體。  
  
2.  在 [物件總管] 中，以滑鼠右鍵按一下模型資料庫的名稱，然後選取**屬性**。  
  
3.  找出屬性， **DirectQueryMode**。 若要啟用關聯式資料來源，這個屬性必須設定為下列其中一個值：  
  
    -   **DirectQuery**  
  
    -   **InMemoryWithDirectQuery**  
  
    -   **DirectQueryWithInMemory**  
  
  
