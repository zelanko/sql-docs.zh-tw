---
title: 在交易式發行集中發行預存程式的執行（SQL Server Management Studio） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publishing [SQL Server replication], stored procedure execution
- stored procedures [SQL Server replication], publishing
ms.assetid: 1d3a3525-0bc5-466f-b097-5359dc74432d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a226d7c58b3b72caf415d8e873b58ca38d3c749f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060430"
---
# <a name="publish-the-execution-of-a-stored-procedure-in-a-transactional-publication-sql-server-management-studio"></a>在交易式發行集中發行預存程序的執行項 (SQL Server Management Studio)
  指定在 [發行項**屬性- \<Article> ** ] 對話方塊中，應該發行預存程式的執行（而不是其定義）。 在 [新增發行集嚮導] 和 [**發行集屬性- \<Publication> ** ] 對話方塊中，可以使用這個對話方塊。 如需使用精靈及存取對話方塊的詳細資訊，請參閱[建立發行集](create-a-publication.md)和[檢視及修改發行集屬性](view-and-modify-publication-properties.md)。  
  
 初始化訂閱時，會將程序的定義 (CREATE PROCEDURE 陳述式) 複寫到訂閱者；在發行者端執行程序時，複寫會在訂閱者端執行對應的程序。  
  
### <a name="to-publish-the-execution-of-a-stored-procedure"></a>若要發行預存程序的執行  
  
1.  在 [**新增**發行集嚮導] 或 [發行集**屬性 \<Publication> -** ] 對話方塊的 [發行項] 頁面上，選取一個預存程式。  
  
2.  按一下 **[發行項屬性]**，然後再按 **[設定反白顯示預存程序的屬性]**。  
  
3.  在 [發行項**屬性 \<Article> -** ] 對話方塊中，針對 [複寫 **] 選項指定**下列其中一個值：  
  
    -   **[預存程序的執行]**  
  
    -   **SP 的序列式交易執行**  
  
         這是建議選項，因為它只會在程序於可序列化的交易內執行時複寫程序執行。 如果預存程序在序列化交易外部執行，則對已發行資料表中所做的資料變更會複寫為一連串的資料管理語言 (DML) 陳述式。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  如果您位於 [**發行集屬性- \<Publication> ** ] 對話方塊中，請按一下 **[確定**] 以儲存並關閉對話方塊。  
  
## <a name="see-also"></a>另請參閱  
 [在異動複寫中發行預存程式執行](../transactional/publishing-stored-procedure-execution-in-transactional-replication.md)  
  
  
