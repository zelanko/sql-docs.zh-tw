---
description: 建立、改變和移除資料庫物件
title: 使用資料庫物件
ms.custom: seo-dt-2019
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
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: adafdf0fe54fd6d942560450f79a8aea0c51beeb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88498535"
---
# <a name="creating-altering-and-removing-database-objects"></a>建立、改變和移除資料庫物件
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  建立 SMO 物件的階段如下：  
  
1.  建立物件的執行個體。  
  
2.  設定物件屬性。  
  
3.  建立子物件的執行個體。  
  
4.  設定子物件屬性。  
  
5.  建立物件。  

 在 SMO 應用程式中建立 SMO 物件的實例時，這些物件不會存在於實例上， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 直到發出 **Create** 方法為止。 但是，不需要為每個個別物件發出 **Create** 方法。 如果物件具有一組子物件，則只需要父物件來執行 **Create** 方法。 例如，資料表的定義要求資料表至少要包含一個資料行才能存在。 同時，如果沒有資料表，資料行無法獨立存在。 在資料表及其資料行之間有一個共同相依的關聯性。  
  
  方法可讓您對物件進行變更。 對於物件的數個變更 (例如，將子物件加入到其中一個物件的集合，或變更屬性值)，會一起進行批次處理，並當做一個變更來執行。 **Alter**方法可減少網路流量並改善整體效能。  
  
 **Drop**語句用來移除一開始建立物件所需的物件及其所有共同相依子物件。  
  
## <a name="see-also"></a>另請參閱  
 [SMO 物件模型](../../../relational-databases/server-management-objects-smo/smo-object-model.md)  
  
  
