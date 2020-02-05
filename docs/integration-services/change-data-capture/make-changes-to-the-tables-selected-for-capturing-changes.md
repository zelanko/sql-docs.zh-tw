---
title: 變更為了擷取變更所選取的資料表 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- makChanToTab
ms.assetid: a309f82a-c6ef-464d-a6ef-df555bfb609a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7ee52054e14c641aad64eaa96b146af86e048d95
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "71298699"
---
# <a name="make-changes-to-the-tables-selected-for-capturing-changes"></a>變更為了擷取變更所選取的資料表

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  在此對話方塊中，您可以從要擷取變更的選定資料表中選取特定資料行。 您也可以編輯 **[安全性角色]** 和 **[擷取執行個體]** 資訊。  
  
 您可以針對您在此對話方塊中為了擷取變更所選取的資料表進行以下變更。  
  
 **對資料行所做的變更會包含在 CDC 執行個體中：**  
  
 執行下列其中一項或兩項作業：  
  
-   選取您要包含的其他任何資料行旁邊的核取方塊。  
  
-   清除您不想再包含的任何資料行旁邊的核取方塊。  
  
 **變更特定資料行的資料類型**：  
  
 您可以針對特定的資料行選取不同的資料類型。 您只能將資料類型變更為與原始資料類型相容的資料類型。  
  
 若要變更資料類型，請按一下 **[資料類型]** 資料行，並選取不同的資料類型。 只能使用與原始資料類型相容的資料類型。  
  
> [!NOTE]  
>  如果沒有其他資料類型可以選擇，就無法使用下拉式清單。  
  
 **變更安全性角色**  
  
 在 **[安全性角色]** 欄位中，輸入新的名稱或是編輯安全性控制角色的名稱。  
  
 **變更或加入擷取執行個體**  
  
 在 **[擷取執行個體]** 欄位中，輸入擷取執行個體的名稱。  
  
## <a name="see-also"></a>另請參閱  
 [如何建立 SQL Server 變更資料庫執行個體](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [選取 Oracle 資料表和資料行](../../integration-services/change-data-capture/select-oracle-tables-and-columns.md)  
  
  
