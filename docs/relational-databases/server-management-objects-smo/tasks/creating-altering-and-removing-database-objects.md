---
title: 使用資料庫物件 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- database objects [SMO]
- objects [SMO]
ms.assetid: 702fd63d-8734-4a02-872e-aecfb037c787
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d218c369c59d3f78ade615ed81048cc99e9a01e8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47815986"
---
# <a name="creating-altering-and-removing-database-objects"></a>建立、改變和移除資料庫物件
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  建立 SMO 物件的階段如下：  
  
1.  建立物件的執行個體。  
  
2.  設定物件屬性。  
  
3.  建立子物件的執行個體。  
  
4.  設定子物件屬性。  
  
5.  建立物件。  
  
 SMO 物件的執行個體建立時在 SMO 應用程式，它們不存在的執行個體上[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]直到**建立**方法發出。 不過，不需要發出**建立**每個個別物件的方法。 如果物件具有一組子物件，父物件，才能執行**建立**方法。 例如，資料表的定義要求資料表至少要包含一個資料行才能存在。 同時，如果沒有資料表，資料行無法獨立存在。 在資料表及其資料行之間有一個共同相依的關聯性。  
  
 <xref:Microsoft.SqlServer.Management.Dmf.Policy.Alter%2A> 方法可讓您對物件進行變更。 對於物件的數個變更 (例如，將子物件加入到其中一個物件的集合，或變更屬性值)，會一起進行批次處理，並當做一個變更來執行。 **Alter**方法會減少網路流量並改善整體效能。  
  
 **卸除**陳述式來移除物件和其所有共同相依子物件所需的一開始建立物件。  
  
## <a name="see-also"></a>另請參閱  
 [SMO 物件模型](../../../relational-databases/server-management-objects-smo/smo-object-model.md)  
  
  
