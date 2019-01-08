---
title: 發行集屬性，資料分割 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.pubproperties.datapartitions.f1
ms.assetid: 5869edb7-d05f-495b-b828-b7fd5e828d20
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 91a11856c8cde6ed94ce2a954ae51c58e4aabf7f
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52752260"
---
# <a name="publication-properties-data-partitions"></a>發行集屬性，資料分割
  **[發行集屬性]** 對話方塊的 **[資料分割]** 頁面，可讓您定義使用參數化篩選之合併式發行集的資料分割。 定義資料分割之後，您可以為這些資料分割產生快照集，依據訂閱者的連接屬性 (登入及/或電腦名稱)，為不同的訂閱者提供不同的初始資料集。 如果訂閱者在第一次同步處理資料分割時沒有可用的快照集，您也可以選取來允許訂閱者要求快照集傳遞和產生。 如需詳細資訊，請參閱 [使用參數化篩選建立合併式發行集的快照集](create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)。  
  
## <a name="options"></a>選項。  
 **加入**  
 按一下 **[加入]** 即可定義資料分割。 在 **[加入資料分割]** 對話方塊中，指定 **HOST_NAME()** 及/或 **SUSER_SNAME()** 的值，並定義排程來重新整理快照集。  
  
 **編輯**  
 在方格中選取現有的資料分割，然後按一下 **[編輯]** 來編輯資料分割。  
  
 **刪除**  
 在方格中選取現有的資料分割，然後按一下 **[刪除]** 來刪除資料分割。  
  
 **立即產生選取的快照集**  
 在方格中選取一或多個資料分割，然後按一下 **[立即產生選取的快照集]** 來產生這些資料分割的快照集。  
  
 **清除現有快照集**  
 在方格中選取一或多個資料分割，然後按一下 **[清除現有快照集]** 來清除這些資料分割的快照集。  
  
 **新的訂閱者嘗試同步處理時，可以視需要自動定義資料分割並產生快照集。**  
 如果您要允許訂閱者要求快照集產生和應用程式，請選取此選項。 如果訂閱者在第一次同步處理資料分割時沒有可用的快照集，則可能需要此選項。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Publication](publish/create-a-publication.md)   
 [檢視及修改發行集屬性](publish/view-and-modify-publication-properties.md)   
 [Parameterized Row Filters](merge/parameterized-filters-parameterized-row-filters.md)   
 [發行資料和資料庫物件](publish/publish-data-and-database-objects.md)   
 [Snapshots for Merge Publications with Parameterized Filters](snapshots-for-merge-publications-with-parameterized-filters.md)  
  
  
