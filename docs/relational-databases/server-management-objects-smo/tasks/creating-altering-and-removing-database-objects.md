---
title: "使用資料庫物件 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- database objects [SMO]
- objects [SMO]
ms.assetid: 702fd63d-8734-4a02-872e-aecfb037c787
caps.latest.revision: "33"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 556403a013ee348e836c059ef9b246b4d5606a87
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/12/2018
---
# <a name="creating-altering-and-removing-database-objects"></a>建立、 改變和移除資料庫物件
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  建立 SMO 物件的階段如下：  
  
1.  建立物件的執行個體。  
  
2.  設定物件屬性。  
  
3.  建立子物件的執行個體。  
  
4.  設定子物件屬性。  
  
5.  建立物件。  
  
 SMO 物件的執行個體建立時在 SMO 應用程式，它們不存在的執行個體上[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]直到**建立**發出方法。 不過，不需要發出**建立**每個個別物件的方法。 如果物件具有一組子物件，父物件，才能執行**建立**方法。 例如，資料表的定義要求資料表至少要包含一個資料行才能存在。 同時，如果沒有資料表，資料行無法獨立存在。 在資料表及其資料行之間有一個共同相依的關聯性。  
  
 <xref:Microsoft.SqlServer.Management.Dmf.Policy.Alter%2A> 方法可讓您對物件進行變更。 對於物件的數個變更 (例如，將子物件加入到其中一個物件的集合，或變更屬性值)，會一起進行批次處理，並當做一個變更來執行。 **Alter**方法可減少網路流量並改善整體效能。  
  
 **卸除**陳述式用來移除物件和其所有共同相依子物件所需一開始建立物件。  
  
## <a name="see-also"></a>另請參閱  
 [SMO 物件模型](../../../relational-databases/server-management-objects-smo/smo-object-model.md)  
  
  
