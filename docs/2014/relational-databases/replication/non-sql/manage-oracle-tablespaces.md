---
title: 管理 Oracle 資料表空間 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], managing tablespaces
- tablespaces [SQL Server replication]
ms.assetid: b8ea6c3b-01d6-4efc-bbfb-03b264530bbd
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a3624aed38a7a5bf75e0c0807aa8d3657156264f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068598"
---
# <a name="manage-oracle-tablespaces"></a>管理 Oracle 資料表空間
  資料表空間是資料庫的儲存單位，大致相當於 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的檔案群組。 資料表空間允許在個別群組中儲存和管理資料庫物件。 如需詳細資訊，請參閱 Oracle 文件集。  
  
 將資料表設定為 Oracle 發行集的一部分，您可以在儲存複寫記錄資訊時選擇性地指定使用現有的 Oracle 資料表空間。 如果未指定，則複寫物件的資料表空間為與複寫管理使用者結構描述相關的預設資料表空間，該複寫管理使用者結構描述在設定「發行者」時設定。  
  
 **為發行項記錄資料表指定資料表空間**：  
  
-   在 **[發行項屬性]** 對話方塊中指定資料表空間。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](../publish/view-and-modify-publication-properties.md)＞。  
  
-   使用 [sp_changearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql)。 若要使用 **sp_changearticle**，請指定下列項目：  
  
    -   參數的 Oracle 發行者名稱 **@publisher** 。  
  
    -   參數的 Oracle 發行集名稱 **@publication** 。  
  
    -   參數的發行項名稱 **@article** 。  
  
    -   參數的 ' 資料表空間 ' 值 **@property** 。  
  
    -   參數的資料表空間名稱 **@value** 。  
  
## <a name="see-also"></a>另請參閱  
 [設定 Oracle 發行者](configure-an-oracle-publisher.md)   
 [在 Oracle 發行者端建立的物件](objects-created-on-the-oracle-publisher.md)  
  
  
