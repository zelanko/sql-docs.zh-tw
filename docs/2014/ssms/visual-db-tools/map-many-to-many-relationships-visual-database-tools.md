---
title: 對應多對多關聯性 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- relationships [SQL Server], many-to-many
- junction tables [SQL Server]
- many-to-many relationships [SQL Server]
- mapping many-to-many relationships [SQL Server]
- database diagrams [SQL Server], relationships
ms.assetid: 2977cf92-98b5-48b2-b0fd-8fbc7040f2b4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a943d0ed7cfb0932f7eec757b40fef4d8de6504c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63306007"
---
# <a name="map-many-to-many-relationships-visual-database-tools"></a>對應多對多關聯性 (Visual Database Tools)
  多對多關聯性可讓您將一個資料表中的每一個資料列，關聯到另一個資料表的多個資料列，反之亦然。 例如，您可以建立 `authors` 資料表和 `titles` 資料表之間的多對多關聯性，以將每一個作者和他/她的書搭配，並將每一本書和所有的作者搭配。 在任一資料表建立一對多關聯性，可能會錯指每一本書只能有一位作者，或每一位作者只能寫一本書。  
  
 資料表之間的多對多關聯性，會藉由聯合資料表在資料庫中進行調整。 聯合資料表包含您要關聯的兩個資料表的主索引鍵資料行。 您可以建立兩個資料表的主索引鍵資料行，與聯合資料表中相符的資料行的關聯性。 在 pubs 資料庫中， `titleauthor` 資料表為聯合資料表。  
  
### <a name="to-create-a-many-to-many-relationship-between-tables"></a>若要建立資料表間的多對多關聯性  
  
1.  在資料庫圖表中，加入您要在其間建立多對多關聯性的資料表。  
  
2.  在圖表上按一下滑鼠右鍵，並從快速鍵功能表選擇 [新增資料表]  ，建立第三個資料表。 這會成為聯合資料表。  
  
3.  在 [選擇名稱]  對話方塊中，變更系統指派的資料表名稱。 例如，`titles` 資料表和 `authors` 資料表之間的聯合資料表，現在的名稱為 `titleauthors`。  
  
4.  將兩個資料表的主索引鍵資料行都複製到聯合資料表。 您可以將其他資料行加入到此資料表，也可以加入到其他資料表。  
  
5.  在聯合資料表中，將主索引鍵設定為包含來自其他兩個資料表的所有主索引鍵資料行。 如需詳細資訊，請參閱[建立主鍵](../../relational-databases/tables/create-primary-keys.md)。  
  
6.  定義兩個主資料表和聯合資料表之間的一對多關聯性。 聯合資料表應該位於所建立的兩個關聯性「多」的一方。 如需詳細資訊，請參閱[建立外鍵關聯](../../relational-databases/tables/create-foreign-key-relationships.md)性。  
  
    > [!NOTE]  
    >  在資料庫圖表中建立聯合資料表，並不會將關聯資料表的資料插入至聯合資料表。 如需將資料插入資料表的詳細資訊，請參閱[建立插入結果查詢 &#40;Visual Database Tools&#41;](visual-database-tools.md)。  
  
## <a name="see-also"></a>另請參閱  
 [使用資料庫圖表 &#40;Visual Database Tools&#41;](work-with-database-diagrams-visual-database-tools.md)  
  
  
