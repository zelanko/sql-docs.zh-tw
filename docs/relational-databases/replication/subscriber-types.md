---
description: 訂閱者類型
title: 訂閱者類型 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.subscribertypes.f1
ms.assetid: a70656cb-21c9-4489-be77-ccd396747e3b
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016
ms.openlocfilehash: 0f6ba4369e2ac2da9058621108f310e1b3f8e953
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97480959"
---
# <a name="subscriber-types"></a>訂閱者類型
[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]
  合併式複寫可讓您指定發行集必須支援的訂閱者類型。 選取訂閱者類型會設定 *發行集相容性層級*，以決定發行集可以使用哪些功能。  
  
 建立發行集快照集之後，可以在 **[發行集屬性]** 對話方塊的 **[一般]** 頁面上增加發行集相容性層級 (設定更多限制)；不可以減少相容性層級。  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]
  
## <a name="options"></a>選項  
 選取此發行集必須支援的每個訂閱者類型。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 發行集可以使用所有的功能。  
  
 [!INCLUDE[ssEW](../../includes/ssew-md.md)]  
 發行集需要快照集檔案為字元格式 (這可由快照集代理程式自動處理)。 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 也有許多與相容性層級無關的限制。  
  
 如果選取此選項，就會啟用發行集的 Web 同步處理選項。 如需有關 Web 同步處理的詳細資訊，請參閱＜ [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [檢視及修改散發者和發行者屬性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
  
  
